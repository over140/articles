### 项目简介

Mixin 是一个免费、快速的点对点跨链数字资产交易网络，可帮助其他区块链分布式账本获得超高 TPS、亚秒级确认、零手续费、加强隐私、无限扩展的能力。

### 基本信息

- 项目启动：2017 年 10 月
- 代币总量：恒定 100 万
- 共识机制：PoS + Asynchronous BFT
- 区块确认：最终确认小于 1 秒
- 数据存储：DAG
- 节点数量：全节点最多 50 个，至少 7 个，目前 32 个
- 挖矿规则：每年矿池剩余 10%
- 安全加固：可信执行环境（TEE）
- 跨链技术：侧链

### 公链特点

- **多重安全**
  PoS 去中心化网络，TEE 硬件加固，数万轻节点监督全节点防止作恶
- **超高并发**
  可直接应用于大型商业应用，性能与传统中心化服务器接近，可通过升级硬件、带宽等实现十万、百万甚至更高 TPS。
- **免费转账**
  用户转账免费，可满足小额支付、消费等商业应用场景。
- **实时到账**
  目前 32 个节点完成一笔转账的校验并签名只需 300 毫秒，不会出现交易回滚、双花等问题。
- **支持丰富**
  现已支持 BTC、ETH、EOS、XMR 等 28 条主链，超过 10 万种代币。
- **管理简单**
  单账户管理多链资产极大简化了用户资产管理的难度，并且默认支持未来新增的公链。
- **多签共管**
  支持最多 255 人共管多签资产，适合团队、家庭共同管理大额资产，也适用于 B2C、C2C平台共管资金，平台无法挪用用户和商家的资金。
- **交易隐私**
  交易只有双方知道，全节点也无法知道交易双方，也就是说无法根据交易本身推导出具体交易双方。
- **更易合规**
  双密钥结构确保资产匿名的同时，用户可以主动提供自己的 view key 供会计查询，可用于报税和会计审计等，而资产不会被转移。
- **生态友好**
  无需许可，接入方便，服务稳定，成本可期。标准的 REST API 接口使得开发者可以以较低的学习成本、任意熟悉的语言快速实现产品和业务，此外最重要的是基于 Mixin 开发应用成本是可以预期的，就像使用 AWS 云服务一样的价格合理性能卓越。
- **网络稳定**
  市面上绝大多数公链都有一个致命的缺陷 — — 节点网络安全受币价影响严重，当币价跌破成本价时节点开始减少进而威胁到网络安全。相比之下，Mixin 的节点通过单独收取 Dapp API 调用费实现长期稳定盈利，类似 AWS 这样的云服务，进而确保了整个网络安全、稳定的持续运行，这也是商业级公链必须具备的特点，相信未来会有更多公链参考 Mixin 的稳定服务模型。

### 核心开发者

核心团队在 2011 ~ 2015 开发的 VPlayer 靠自增长全球获得 4000 万用户，期间发布的 Vitamio SDK 更是被微博、猎豹、金山、酷 6 等多家知名企业授权使用；2015 ~ 2017 开发的 Shou.TV 手游直播获得了全球 1000 万用户。

- 冯晓东 — — CEO & 联合创始人
  音视频专家，精通 Go 、Ruby、Android 等全栈开发，对产品有深刻的理解。大三辍学做 Android App 在 Google Play 收入达到 100 万美金，后加入一下科技负责 VPlayer 和 Vitamio，2014 年成立新公司专注海外手机游戏直播。
- 宋晓明 — — CTO & 联合创始人
  前一下科技研究院院长，负责视频播放底层相关产品线的研发，对 Android 和 iOS 音视频有深刻的理解，帮助公司完成 Vitamio 与微博、猎豹等数亿用户产品线对接。
- 唐俊 — — 产品总监 & 联合创始人
  前一下科技秒拍 Android 研发经理，拥有丰富的 Android 和 iOS 开发经验，对用户体验有深刻认识。

### 核心技术

- 跨链记账
  侧链会同步并监听主链上所有与 Mixin 相关的交易，所有外部充值、提现和内部转账都被记录在去中心化的分布式账本上，而主链资产被转入由全节点共同管理的多重签名地址。每一笔记录都包含了资产类型（例如比特币、以太坊等）、转账金额等信息，不可篡改可追溯。注意 Mixin 没有发币功能所以也没有主网代币，不会凭空产生资产。

![](https://wg.isdot.net/api/un/img?key=user-upload/12123326/5d1bd481e18433ef.png)

Mixin 跨链方案和交易所有些类似，但是是由去中心化的节点共同管理资产，代码、数据公开透明，并且专注转账这一件事。

- 有向无环图技术（DAG）
  Mixin 采用 DAG 作为底层数据结构模型，区别于其他 DAG 公链（例如 IOTA、Bytaball 等），Mixin 没有中心权威节点，数据不需要等待中心权威节点的最终确认。通过限制引用数据的时间等机制确保异步高效运行，并通过 Asynchronous BFT 来保证了共识结果的正确性。可以简单理解 Mixin 每个全节点都是一条链，具备完整的数据，但数据的顺序是不同的，最终都能推导出同样的结果：

![DAG](https://wg.isdot.net/api/un/img?key=user-upload/12123326/012dd402cba298a5.png)

- 可信执行环境（TEE）  
  Mixin 使用 Intel SGX 作为 TEE 的实现来进一步提升安全性，所有全节点都必须在可信执行环境中运行，确保全节点 “正在运行的代码” 的确是 “它声称正在运行的代码”，没有人能够在不被察觉的情况下改变可信执行环境里正在运行的代码。
  ![](https://upload-images.jianshu.io/upload_images/647864-695ddd48e04a53e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

- 隐私增强
  通过 CryptoNote 技术加强 UTXO 交易隐私，交易只有双方知道，全节点也无法知道交易双方，也就是说无法根据交易本身推导出交易具体双方:

![CryptoNote](https://wg.isdot.net/api/un/img?key=user-upload/12123326/8534d4fcaf06c905.png)

**总结：有限 PoS 节点数量、DAG、UTXO、Asynchronous BFT、CryptoNote、TEE 这一系列技术精妙的组合不仅实现了数据的不可篡改性，还解决了性能瓶颈、双花、隐私、可扩展等问题。**

### 节点网络

##### 全节点

全节点主要负责记账，校验并签名每一笔交易，每笔交易都需要经过三分之二加一的节点校验和签名才会最终生效，截止到 2020-02-12 共计 32 个全节点稳定运行中。

- 加入节点
  无需许可，可匿名参与，抵押上一年流通量的 2% 即可加入。例如第一年加入全节点需要 10,000 XIN，第二年可能需要 11,000 XIN 左右；参与全节点的硬件设备按 8 核 CPU + 32 G 内存 + 500G SSD 硬盘 + 100 M带宽每月费用不到 500 美金。
- 退出节点
  无需许可，退出节点需要扣除抵押的 1% 作为手续费

##### 轻节点

轻节点也需要抵押，作用主要是监督全节点记账，并安排自动投票。

### XIN  代币

##### 分配

- 50%矿池节点激励
- 40% 统一以 1 XIN / 20 EOS 的价格通过交易所公开出售给支持者，无天使、无基石、无私募
- 5% 奖励白名单用户
- 5% 核心开发团队

##### 流通

截止到 2019 年 11 月，矿池未流通约为 48 万，目前每天挖矿释放 123 XIN 且呈逐年递减趋势，已流通 XIN 约为 52 万：

- 节点抵押 31 万，其中散户众筹节点多达 15 个，其他的主要是机构和其他团队，例如昂达集团、老猫团队等
- Domain 抵押了 5 万，核心开发团队所持有的 5 万 XIN 已全部抵押
- 市面流通 16 万，主要是交易所、节点排队、钱包等

##### 用途

- 抵押参与全节点记账，并获得挖矿收益和超额手续费分配
- 抵押参与轻节点，监督全节点记账并安排自动投票
- 抵押参与 Domain 资产管理，与节点共同管理资产
- 投票参与到社区治理，例如投票确定作恶节点惩罚金额、接入什么链、内核规范或者是升级过程中的某些策略等。
- 创建 Dapp 需要一次性消耗一些 XIN ，具体费用由 Dapp 声称消耗的资源决定。
- 节点可自行决定 API 调用是否按市价以 XIN 的形式结算（节点超额手续费分配是按 XIN 来结算的）

##### 交易所

- [BigONE](https://big.one/trade/XIN-EOS)，XIN 目前主要在 BigONE 交易，早期 IEO 也是在这里进行，交易所也帮助许多用户参与了节点共建。
- [BitZ](https://www.bit-z.com/exchange/xin_usdt)
- [CBX](https://www.bit-z.com/exchange/xin_btc)
- [WhaleEx 鲸交所](https://www.whaleex.com/trade/XIN_EOS)

**XIN 代币总量恒定 100 万不增发，用途如上所述没有什么暴涨逻辑，和股份有点类似，抵押参与记账然后持续稳定赚取利润。支持 Mixin 项目不一定需要购买 XIN ，下载使用 Mixin 钱包就是最好的方式之一！**

### Dapps

- [Mixin Messenger](https://mixin.one/messenger)
  Mixin Messenger 是 Mixin Network 第一个开源的 Dapp ，除了好用的端对端加密聊天，还集成了安全简单的全币种钱包。
- [OceanONE](http://ocean.one)
  基于 Mixin Network 的开源去中心化交易所，拥有中心化交易所类似的体验。实时挂单、买单和撤单，Mixin Network 所有币种都可以与 XIN、BTC 和 Omni USDT 交易，交易记录上链可查可追溯，交易完资产自动返回用户的钱包。BigDEX 和 FoxONE 基于此进行了二次开发。
- [Exin.ONE](https://exin.one)
  基于 Mixin Network 的一站式数字资产金融服务平台，提供 C2C 、币币交易、定投、余币宝等多项服务，积累数万用户、完成超过 20 万比订单，深受用户好评。
- [Fox.ONE](https://fox.one)
  基于 Mixin Network 的一款数字资产 App，融合了交易所、钱包、行情、资讯等。
- [币印矿池](https://poolin.com)
  全球排名前三的矿池，支持全主流币种挖矿的专业矿池，现服务于全网大部分的比特币算力。矿工设置 Mixin Messenger 为收款地址可享受零起付额，节省大量手续费，日挖日卖成为可能。
- [B.Watch](https://b.watch)
  BOX 是一个完全公开、透明、零管理费基于 Mixin Network 发行的 ETF 基金产品，由李笑来设计、发行，https://b.watch 是 BOX 的社区。付费定投践行群超过 3400 人， 已申购超过 1200 万 BOX，净值超过 2500 万美元，社区鼓励定投践行者们只买不卖，并且长期持有 BOX 两个大周期以上（预计 5 - 8 年）。
- [BigDEX](http://dex.big.one)
  BigDEX 是基于 Mixin Network 的去中心化交易所，BigONE 重要战略产品之一，拥有”简单、跨链、快速、透明“四大特性，支持用户自主上币，现在挂单还可以赚手续费。
- [CoinView（币观）](https://zh.coinjinja.com/coinview)
  日本用户量最大的第三方虚拟货币工具信息App，信息最全面的 STO/ICO 信息平台。CoinView 在 App Store 收获了 9600 位以上的用户评价，平均分超过 4.6 分。
- [Press.ONE](https://press.one)
  基于区块链的分布式数字内容交易及分发网络
- [W3c.Group](https://w3c.group)
  W3c.Group 是一个区块链技术为主导的开发者社区， 将 WGT 和积分（主要涉及挖矿）的流动情况都在 Mixin Network 中进行了存证，使得 W3c.Group 能够变得更公开透明。

### 路线图

- 2017 年 9 月项目筹备
- 2018 年 1 月 Mixin Messenger 上线
- 2018 年 8 月 去中心化交易所 OceanONE上线并开源
- 2018 年 9 月 测试网络发布
- 2018 年 11 月 举办首届全球开发者大会
- 2019 年 2 月 主网正式上线
- 2019 年 7 月 主网升级至 0.5.0 版本，性能提升 80%，存储空间减少 50%
- 2019 年 9 月上线全球知名漏洞众测平台 HackerOne

### 统计数据

以下信息统计截止到 2020-05-04 ：

- 支持 BTC、ETH、EOS、DASH、XRP、XEM、SC、DOGE、BCH、LTC、ZEC、ETC、ZEN、TRON、XLM、MGD、BTM、ATOM、BSV、DCR、BNB、XMR、BTS、RVN、Grin、VCASH、CKB、HNS 共计 28 条主链，超过 10 万种代币。
- 项目自发布以来总转账次数 432,819,685
- 网络总资产市值超过 7700 万美元（不计 XIN 和 BOX），其中包括 5,700 BTC、490 万 EOS、15,600 ETH 等。
- Mixin 团队保持在十几个人的规模，以研发为主， 100 万美元足够团队花 1 年。
- Mixin API 服务请求目前一天使用的流量是 150GB 左右，不包括图片、视频和文件等。

### 公开信息

- 白皮书：https://mixin.one/assets/Mixin-Draft-2018-07-01.pdf
- 智能合约（已通过安全审计）：https://etherscan.io/token/0xa974c709cfb4566686553a20790685a47aceaa33
- 区块浏览器：https://mixin.one/snapshots 、 https://blockchair.com/mixin（第三方，信息非常全）
- 公链状态：https://mixin.one/network/chains
- 热门资产信息：https://mixin.one/network/assets
- 资产排名 Top 100 ：https://api.mixin.one/network/assets/top
- 全网转账记录：https://developers.mixin.one/api/alpha-mixin-network/network-snapshots
- 全网充值记录：https://developers.mixin.one/api/alpha-mixin-network/external-transactions
- 完整的一笔主网转账信息：http://api.mixinwallet.com/transactions/f19b16411137acde87d0633fc8d61fabcc7632938b166d9d085558c32cf628f1

### FAQ

- Mixin 、Mixin Network 与 Mixin Messenger 什么关系？
  Mixin 是 Mixin Network 的简称，Mixin Messenger 是 Mixin Network 上第一个开源的 Dapp。由于历史原因，很长一段时间内 Mixin 被认为是 Mixin Messenger 。

- 免费转账大量发起垃圾交易怎么办？
  节点会向 Dapp 收取 API 调用费，参见扩展阅读 [Mixin Network 全节点的稳定经济模型](https://www.jianshu.com/p/12032052d560)。

- 白皮书里万亿 TPS 是怎么理解？
  其实是用一个数字来形容 Mixin Network 的 TPS 没有理论上限，主网分布式网络的性能与传统服务器集群性能接近，可以简单的通过升级硬件和带宽、优化算法不断提升 TPS ，很容易就达到十万、百万甚至更高 TPS。理论没有上限这点很重要，不像 BTC 理论上限是非常有限的，你只能达到那个速度，现在全节点服务器中低配置就轻松达到了 3000 TPS。

- 为什么我钱包里 BTC 充值地址在区块链浏览器链上查不到余额？
  Mixin 的充值和提现不是同一个地址，用户充值后资产会按需转移至由所有全节点管理的多签地址，提现的时候需要超过 2/3 + 1 节点校验并签名后再从多签地址提现至目标地址。

- 如何检查 Mixin 里的资产是真的链上资产？比如 BTC 
  Mixin 不会凭空产生资产，所有的资产都是通过外部充值进入 Mixin 网络，用户充值后资产会按需转移至由所有全节点管理的多签地址。如果想检查 Mixin 链上资产以 BTC 为例，需要累加 https://btc.com/1zgmvYi5x1wy3hUh7AjKgpcVgpA8Lj9FA 这个多签地址里所有转入地址的余额再加上多签地址的余额，该数值不会等于 https://mixin.one/network/assets 里 BTC 的数量，因为有些地址的资产还没有被归集所以没有累加到。

### 开发者

如果你是开发者，Mixin 对你来说是一个巨大的机会，越早加入越容易获得珍贵的种子用户，用你熟悉的语言开发有价值的应用，提供好的服务然后稳定的赚钱，与 Mixin 共同成长！

- 基于 Mixin Network 开发 Dapp 
  参见文档 [Mixin 全币种钱包接入指南](https://w3c.group/c/1571124858462233)
- 基于 Mixin Messenger 开发小程序机器人
  参见文档 [Mixin Messenger 机器人接入指南](https://w3c.group/c/1567337919309762)
- 基于 OceanONE 开发去中心化交易所 
  参加文档 [基于 OceanONE 开发去中心化交易所](https://www.jianshu.com/p/e197cbade157)

### 长期活动

- 提现手续费**全额**补贴
  所有 Dapp 开发者享有提现手续费全额按月返现，钱包用户可以通过 Exin 或 Fox 提现来申请领取提现手续费返回。

### 体验钱包

![](https://mixin.one/assets/14a354d19d44b0e467f9f7481ba8b167.png)

##### Android 用户

- Google Play 下载：https://play.google.com/store/apps/details?id=one.mixin.messenger

- 应用宝下载：https://a.app.qq.com/o/simple.jsp?pkgname=one.mixin.messenger

- 直接 APK 下载：https://download.exin.one/mixin/android/ （Exin 提供）
  
  ##### iOS 用户

- 【推荐】海外 Apple ID：https://itunes.apple.com/app/mixin/id1322324266

- 【推荐】TestFlight： 私信 762532 申请加入，有完整版钱包功能。

- 中国 Apple ID：https://apps.apple.com/cn/app/mixin/id1457938019 没有内置钱包功能，可以搭配使用机器人小钱包。

### 关注 Mixin 社区

- 官网：https://mixin.one
- 微博：https://weibo.com/MixinNetwork
- Twitter：https://twitter.com/Mixin_Network
- Reddit：https://www.reddit.com/r/mixin
- Medium：https://medium.com/mixinnetwork
- Github: https://github.com/MixinNetwork
- Mixin Messenger：搜索机器人 7000101914 订阅 「 Mixin 产品动态」

### 扩展阅读

- [Mixin Network 全节点的稳定经济模型](https://www.jianshu.com/p/12032052d560)
- [热门跨链项目大比拼 - Polkadot vs Mixin vs Cosmos](https://www.jianshu.com/p/4140e0c6e4a3)
- [Mixin Network 是 PoS 版的比特币网络](https://www.jianshu.com/p/ed64085d5861)
- [欢迎使用 Mixin Messenger 可信多链钱包](https://w3c.group/c/1566284250545868)
- [Mixin Messenger 的分布式 D3M-PIN 码设计方案](https://w3c.group/c/1575723828153220)

----

我是长老，欢迎来 Mixin Messenger 找我聊天，我的 Mixin ID: 762532 。 
