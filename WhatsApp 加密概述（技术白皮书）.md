### 简介

本白皮书提供了 WhatsApp 端到端加密系统的技术说明。请访问 WhatsApp 的网站 www.whatsapp.com/security 了解更多。

WhatsApp Messenger 允许人们自由的交换消息（包括聊天，群聊，图片，视频，语音消息和文件），并在发送者和接收者之间使用端对端加密（在 2016 年 3 月 31 之后的版本）。

Signal 协议是由 Open Whisper Systems （非盈利软件开发团体）设计，是 WhatsApp 端对端加密的基础。这种端对端加密协议旨在防止第三方和 WhatsApp 对消息或通话进行明文访问。更重要的是，即使用户设备的密钥泄露，也不能解密之前传输的消息。

本文档概述了 Singal 协议在 WhatsApp 中的应用。

### 术语

##### 公钥类型

- 身份密钥对（Identity Key Pair） —— 一个长期 Curve25519 密钥对，安装时生成。
- 已签名的预共享密钥（Signed Pre Key） —— 一个中期 Curve25519 密钥对，安装时生成，由身份密钥签名，并定期进行轮换。
- 一次性预共享密钥（One-Time Pre Keys） —— 一次性使用的 Curve25519 密钥对队列，安装时生成，不足时补充。

##### 会话密钥类型

- 根密钥（Root Key） ——  32 字节的值，用于创建链密钥。
- 链密钥（Chain Key） —— 32 字节的值，用于创建消息密钥。                                                                                                                                                                  
- 消息密钥（Message Key） —— 80 个字节的值，用于加密消息内容。32 个字节用于 AES-256 密钥，32 个字节用于 HMAC-SHA256 密钥，16 个字节用于 IV。

### 客户端注册

在注册时，WhatsApp 客户端将身份公钥（public Identity Key）、已签名的预共享公钥（public Signed Pre Key）和一批一次性预共享公钥（One-Time Pre Keys）发送给服务器。WhatsApp 服务器存储用户身份相关的公钥。WhatsApp 服务器无法访问任何客户端的私钥。 

### 会话初始化设置

要与另一个 WhatsApp 用户通信，WhatsApp 客户端需要先建立一个加密会话。加密会话一旦被创建，客户端就不需要再重复创建会话，除非会话失效（例如重新安装应用或更换设备）。

建立会话：

1. 会话发起人为接收人申请身份公钥（public Identity Key）、已签名的预共享公钥（public Signed Pre Key）和一个一次性预共享密钥（One-Time Pre Key）。
2. 服务器返回所请求的公钥。一次性预共享密钥（One-Time Pre Key）仅使用一次，因此请求完成后将从服务器删除。如果一次性预共享密钥（One-Time Pre Key）被用完且尚未补充，则返回空。
3. 发起人将接收人的身份密钥（Identity Key）存为 **I**recipient，将已签名的预共享密钥（Signed Pre Key）存为 **S**recipient，将一次性预共享密钥（One-Time Pre Key）存为 **O**recipient。
4. 发起者生成一个临时的 Curve25519 密钥对 —— **E**initiator
5. 发起者加载自己的身份密钥（Identity Key）作为 **I**initiator
6. 发起者计算主密钥 master_secret = ECDH ( **I**initiator, **S**recipient ) || ECDH ( **E**initiator, **I**recipient ) || ECDH ( **E**initiator, **S**recipient )  || ECDH ( **E**initiator, **O**recipient ) 。如果没有一次性预共享密钥（One-Time Pre Key），最终 ECDH 将被忽略。
7. 发起者使用 HKDF 算法从 master_secret 创建一个根密钥（Root Key）和链密钥（Chain Keys）。

### 接收会话设置

在建立长期加密会话后，发起人可以立即向接收人发送消息，即使接收人处理离线状态。在接收方响应之前，发起方所有的消息都会包含创建会话所需的信息（在消息的 header 里）。其中包括发起人的 Einitiator 和 Iinitiator 。当接收方收到包含会话设置的消息时：

1. 接收人使用自己的私钥和消息 header 里的公钥来计算相应的主密钥
2. 接收人删除发起人使用的一次性预共享密钥（One-Time Pre Key）
3. 发起人使用 HKDF 算法从主密钥派生出相应的根密钥（Root Key）和链密钥（Chain Keys）

### 交换消息

一旦建立了会话，通过 AES256 消息密钥加密（CbC 模式）和 HMAC-SHA256 验证来保护客户端交换消息。

消息密钥是短暂的且在每次发送消息后都会变化，使得用于加密消息的消息密钥不能从已发送或已接收后的会话状态中重建。

消息密钥在发送消息时对发送人的链密钥（Chain Key）进行向前的“棘轮（ratchets）”派生而来。此外，每次消息巡回都执行一个新的 ECDH 协议以创建一个新的链密钥（Chain Key）。通过组合即时 “哈希棘轮（hash ratchet）” 和巡回 “DH 棘轮（DH ratchet）” 提供前向安全。

### 通过链密钥（Chain Key）计算消息密钥（Message Key）

消息发送者每次需要新的消息密钥时，计算如下：

1. 消息密钥（Message Key）= HMAC-SHA256(Chain Key, 0x01)
2. 链密钥（Chain Key）随后更新为： 链密钥（Chain Key） = HMAC-SHA256(Chain Key, 0x02)

这样形成向前“棘轮（ratchets）”链密钥（Chain Key），这也意味不能使用存储的消息密钥推导出当前或过去的链密钥（Chain Key）值。

### 通过根密钥（Root Key）计算链密钥（Chain Key）

每一条发送的消息都附带一个短期的 Curve25519 公钥。一旦收到响应，新的链密钥（Chain Key）计算如下：

1. ephemeral_secret = ECDH(Ephemeralsender, Ephemeralrecipient)
2. 链密钥（Chain Key），根密钥（Root Key）= HKDF(Root Key, ephemeral_secret)

一个链密钥只能给一个用户发消息，所以消息密钥不能被重用。由于消息密钥和链密钥（Chain Keys）的计算方式，消息可能会延迟、乱序或完全丢失而不会有问题。

### 传输媒体和附件

任何类型的大附件（视频，音频，图像或文件）也都是端对端加密的：

1. 发件人（发消息的 WhatsApp 用户）生成一个 32 字节的 AES256 临时密钥和一个 32 字节HMAC-SHA256 临时密钥。
2. 发件人通过 AES256 密钥（CBC 模式）和随机 IV 给附件加密，然后附加使用 HMAC-SHA256 密文的 MAC。
3. 发件人将加密的附件以上传到服务器以二进制存储。
4. 发件人给收件人发送一个包含加密密钥、HMAC 密钥、加密二进制的 SHA256 哈希值和指向二进制存储的指针的加密消息
5. 收件人解密消息，从服务器检索加密的二进制数据，验证 AES256 哈希，验证 MAC并解密为明文。

### 群组消息

传统未加密的聊天应用通常对群组消息使用“服务器扇出（server-side fan-out）”来发群组消息。当一个用户向群组发消息时，服务器将消息分发给每一个群组成员。

而“客户端扇出（client-side fan-out）”是客户端将消息发给每一个群组成员。

WhatsApp 的群组消息基于上面列出的成对加密会话构建，以便高效实现大量群组消息通过服务器扇出（server-side fan-out）。这是通过 Signal 传输协议（Signal Messaging Protocol）的 “发送者密钥（Sender Keys）”来完成的。

WhatsApp 群组成员第一次发消息到群组：

1. 发送人生成一个随机 32 字节的链密钥（Chain Key）。
2. 发送人生成一个随机 Curve25519 签名密钥对。
3. 发送人将 32 位链密钥（Chain Key）和签名密钥中的公钥组合成消息发送人密钥（Sender Key）。
4. 发件人用成对传输协议为每个群组成员单独加密发送人密钥（Sender Keys）。

所有后续发给该群组的消息：

1. 发送人从链密钥（Chain Key）中获取消息密钥（Message Key）并更新链密钥（Chain Key）
2. 发送人在 CbC 模式下使用 AES256 加密消息
3. 发送人使用签名密钥（Signature Key）签名密文
4. 发送人将单个密文消息发给服务器，服务器将消息分发给所有群组成员

消息发送人链密钥（Chain Key）的“哈希棘轮（hash ratchet）”提供向前安全。当群组成员离开时时，所有剩下的群组成员都清除发送人密钥（Sender Key）并重新生成。

### 通话设置

WhatsApp 语音和视频通话也是端对端加密。当 WhatsApp 用户发起语音或视频通话时：

1. 发起人与接收人建立加密会话（如果还没有建立过）
2. 发起人生成一个随机 32 字节的安全实时传输协议（SRTP） 主密钥（master secret）
3. 发起人向接收人发送一个包含安全实时传输协议（SRTP）主密钥的加密消息用于发通话信号
4. 如果应答了呼叫，跟着发起安全实时传输协议（SRTP）呼叫

### 状态

WhatsApp 状态加密方式和群组消息非常相似。给指定的一组接收人第一次发状态遵循向群组第一次发消息相同的步骤。类似地，给同一组接收人发送后续状态也遵循发群组消息相同的步骤。当状态发送人更改状态隐私设置或从地址簿种删除号码来删除接收人时，状态发送人会清除发送人密钥（Sender Key）并重新生成。

### 实时位置

> 待填坑

### 验证密钥

WhatsApp 用户还可以验证与之通信用户的密钥，以便他们能够确认未授权的第三方（或 WhatsApp）未发起中间人攻击。通过扫描二维码或通过比较 60 位数字来完成。
二维码包括：

- 版本号
- 双方的用户身份
- 双方完整的 32 字节身份公钥

当用户扫描对方的二维码时，将比较这些密钥以确保二维码中的身份密钥与服务器检索到的相匹配。

通过拼接两个用户身份密钥的 30 位数字指纹来计算 60 位数字号码。计算 30 位数字指纹步骤：

1. 重复 SHA-512 哈希身份公钥和用户标识符 5200 次
2. 获取最后输出哈希的前 30 个字节
3. 将 30 个字节分成 6 组每组 5 字节的数据块
4. 通过解析每组 5 字节数据块为 big-endian 无符号整形并且取模 10 万次转换为 5 个数字
5. 把六组每组 5 个数字连接成 30 位数字

### 传输安全

WhatsApp 客户端和服务器之间所有通信都在单独的加密通道内分层。在 Windows Phone、iPhone 和 Android 上，这些端对端加密客户端可以使用噪音管道（Noise Pipes），使用噪声协议框架（Noise Protocol Framework）中的 Curve25519、AES-GCM 和 SHA256 实现长期运行的交互连接。

这为客户端提供了一些不错的属性：

- 极快的轻量级连接设置和恢复
- 加密隐藏元数据防止未授权的网络监听。没有透露连接用户身份相关的信息。
- 服务器上不存储客户端的安全认证信息。客户端使用 Curve25519 密钥进行身份验证，因此服务器仅保存客户端认证公钥（public authentication key）。如果服务器的用户数据库被入侵，也不会泄露个人认证凭证。

### 结论

WhatsApp 用户之间的消息受到端对端加密协议的保护，因此第三方和 WhatsApp 都无法获知消息内容，消息只能由接收人解密。所有 WhatsApp 消息（包括聊天、群聊、图片、视频、语音消息和文件）和 WhatsApp 通话都受到端对端加密的保护。

WhatsApp 服务器无法访问 WhatsApp 用户的私钥，并且 WhatsApp 用户可以选择验证密钥以确保其通讯完整。

WhatsApp 使用的 Signal 协议库是开源的，代码：https://github.com/whispersystems/libsignal-protocol-java/

### 参考

- [维基百科：端到端加密](https://zh.wikipedia.org/wiki/%E7%AB%AF%E5%88%B0%E7%AB%AF%E5%8A%A0%E5%AF%86)
- [Signal 协议中的双棘轮算法](https://blog.lancitou.net/double-ratchet-algorithm/#double-ratchet)

------------

译者水平有限，希望对英语不好的朋友有一点帮助。
