# 热门跨链项目大比拼 - Polkadot vs Mixin vs Cosmos

伴随着区块链的发展，各种钱包伴随着不同链大量涌现，许多用户干脆把代币放在交易所，而中心化交易所频繁失窃让用户损失惨重。侧链技术的出现使多链钱包成为可能，使用方便、转账快还极大的减少了原链的网络拥堵情况。有了多链会立刻想到跨链，国外的 Polkadot、 Cosmos 和国内的 Mixin 等都是跨链的前沿实践者，下文收集、整理对比一下这三个项目，时间仓促难免资料有不准确甚至错误之处，欢迎联系作者纠正。

跨链更大的愿景在于价值交换和跨链协作，结合不同原链的智能合约和应用程序无缝实现更灵活、更完整、可扩展的商业系统，实现更大的商业价值，促进整个区块链网络的发展最终服务于用户。

### 术语

原链：一般指接入跨链系统的链，比如比特币网络、以太坊、Zcash 等
侧链：一般指成为原链的一个节点，主要用于监听跟自己相关的交易，然后记录到本链上
代币：Coin 和 Token 的统称
挖矿：Staking 的意思，也可以理解为抵押。PoS 其实没有挖矿这一说，为了方便说明会用这个词

### 基本信息

- Polkadot
  口号： 可扩展的异构多链系统
  官网：https://polkadot.network
  跨链：侧链、中继
  共识：GRANDPA（GHOST-based Recursive ANcestor Deriving Prefix Agreement）/ BABE（Blind Assignment for Blockchain Extension）
  区块链：中继链 Relaychain
  CMC 排名：预计前 30 ，代币被锁定至 2019 年第三季度才能上市交易
  代币总量：初始总量 1000 万，年增发率 10% ~ 100%
  Twitter 粉丝：2.8 万

- Mixin 
  口号：一个免费、快速的点对点数字资产交易网络
  官网：https://mixin.one
  跨链：侧链、Layer2 Off-Chain
  共识：Asynchronous BFT
  区块链：Mixin 内核 Mixin Kernel，用 DAG 存储交易记录
  CMC 排名：69（2019-04-26）
  代币总量：恒定 100 万
  Twitter 粉丝：0.4 万

- Cosmos
  口号：区块链的互联网
  官网：https://cosmos.network
  跨链：侧链、中继
  共识：Tendermint（BFT）
  区块链：Cosmos Hub
  CMC 排名：15（2019-05-01）
  代币总量：初始总量 2 亿，年增发率 7% ~ 20%
  Twitter 粉丝：2.3 万

### 代币

##### 代币分发

- Polkadot 代币 DOT 初始总量 1000 万，其中 500 万已于 2017 年秋季以私募 + 公募的方式完成销售，所有投资者都进行了 KYC 认证并排除了中国和美国的投资者，公募部分采取荷兰式拍卖方式以 10.4 DOTs / 1 ETH (约 196 人民币)的价格完成众筹；200 万预计将于 2019 年上线前销售；剩余的 300 万将由 Web3 基金会持有。— —  **第一次募集了 48 万个 ETH，但其中 30 万由于漏洞被冻结至今，第二次融资待定（预计销售 6000 万美元）**

- Mixin 代币 XIN 总量 100 万恒定，其中 40 万已于 2017 年 11 月以 1 XIN / 20 EOS（约 258 人民币，当时 EOS 1.9 美元一个）的价格通过交易所出售给支持者，挖矿预留 50 万，早期支持者 5 万，团队 5 万。 — — **募资 800 万 EOS**

- Cosmos 代币 ATOM 初始总量 2 亿，其中 75% 于 2017 年 4 月以 0.1 美元的价格完成公募（战略投资人和早期投资者分别有 25% 和 15% 的折扣），Interchain 基金会 10% ，All in Bits 公司 10%，天使投资人占 5%。 — — **募资 25 万 ETH 和 4870 BTC**

##### 代币增发

- DOT 代币的年增发率 10% ~ 100%
- XIN 代币不增发，总量恒定
- ATOM 代币的年增发率 7% ~ 20% （视 ATOM 抵押率而定，Staking 模式能有效地抵御高增发、高通胀下的代币价值稀释，如果你不想交易，务必参与到 Staking 里避免被通膨稀释）

##### 代币用途

- DOT 持有者能够参与社区治理，比如投票；促进共识达成，惩罚作恶参与者，奖励积极参与者；用于抵押添加新的平行链。

- XIN 持有者能够参与社区治理；促进共识达成，惩罚作恶全节点，奖励节点诚实工作。节点矿池支出：抵押 XIN 做全节点和轻节点赚取 XIN；节点矿池收入：创建 Dapp 、 API 调用、全节点退出、全节点作恶罚没。可以看出 Mixin 的免交易手续费其实也不免费，是通过收取 Dapp 的 API 调用收费来限制垃圾交易

- ATOM 持有者能够参与社区治理，抵押参与投票；促进共识达成，惩罚作恶验证人，奖励诚实验证人。可用于支付交易手续费（注意 Cosmos Hub 验证人可以接受任何种类的代币或组合作为处理交易的费用）

> 大部分的代币其实是没有什么升值逻辑，这三个项目也不例外，仅仅是用于社区治理、达成共识和经济模型需要，对于持有者而言主要用于参与投票决策和抵押 + 额外的投入赚取更多代币（例如节点），系统通过手续费消耗、罚没减少代币或奖励来促进代币流通。Polkadot 和 Cosmos 除了代币增发激励收入还有交易手续费分配；Mixin 只有挖矿激励没有交易手续费分配（实际上回收进矿池了），但是在提现的时候会多收用户原链手续费作为额外收入分配给节点，据悉上线以来已发生 5000 比以太坊提现并累积多收了 90 ETH 可供分配。

### 链上治理

- Polkadot  持币用户都可以通过抵押发起或支持全民提案、全民公投和议员选举，一段时间内抵押数量最多的提案进入全民公投（自动返回前面的抵押），议会可以投票否则或取消全民公投。注意投票除了跟抵押数量有关，还跟抵押时间正相关。

- Mixin 的持币用户可以通过投票参与到社区治理中，例如投票确定作恶节点惩罚金额、接入什么链、内核规范或者是升级过程中的某些策略等。

- Cosmos  持币用户都可以通过抵押发起验证人选举、投票决策网络协议上的各类变动。注意所有的验证者都需要对所有提案进行投票，如果没能及时对提案做出投票会有缺席惩罚。Cosmos Zone 拥有自治权可有自己的一套章程及管理机制，但是不能违背 Cosmos Hub 的章程和管理机制。

> 三个项目都是链上治理，Polkadot 和 Cosmos 的选举能促进用户参与的积极性，帮项目起到了很好的宣传作用。

### 创始人

- Gavin Wood — — Parity Technologies 的 CTO，英国约克大学计算机科学博士，以太坊联合创始人 CTO，撰写以太坊黄皮书，几乎一个人写完最早以太坊客户端 cpp-ethereum，发明了智能合约开发设计高级语言 Solidity

- 冯晓东 — — Mixin 的 CEO 与创始人，资深区块链开发专家和音视频专家，带领团队开发 Mixin 主网；曾独立花不到 1 月时间完成 BigONE 交易所；前 ShouTV 手游直播 CEO，产品用户过千万；前一下科技总经理，产品 VPlayer 海内外用户超过 4000 万，SDK 产品 Vitamio 间接用户 15 亿，被集成到数千个产品中，其中不乏微博、金山、猎豹等这样的知名企业

- Jae Kwon — — Tendermint 的 CEO 与创始人，拥有康奈尔大学的计算机学位，带领团队开发 Cosmos 网络。

### 项目进度

- Polkadot 主网未上线，已经发布 POC-1、POC-2、POC-3、PoC-4 测试网络
- Mixin 主网已上线，主要是转账功能，已支持 13 条热门主链，但资产迁移尚未完成，节点自由出入、接入 Domain、支持智能合约调用等尚未完成
- Cosmos 主网已上线，Cosmos SDK 已经可用，IBC 和社区治理还未开发完

### 生态系统

- Polkadot
  ChainX、ChainLink、0x protocol、Blink Network、Aragon、AdEx 等 23 个项目，参考[这里](https://forum.web3.foundation/t/teams-building-on-polkadot/67)
- Mixin 
  CoinView、CandyONE、FoxONE、OceanONE、ExinONE、ONO、PressONE
- Cosmos 
  Binance Chain、Sentinel、IRISnet、Lino Network、Terra、Loom 等多达八十多个项目

### 节点

- Polkadot 的无上限，测试网络 Alexander 现在有 80 个节点，随着原链的接入增多而增多
- Mixin 的节点分为全节点和轻节点，目前有 15 个全节点，后期预计稳定在 30 个左右，全节点最少 7 个，最多 50 个。抵押流通量的 2% 即可加入全节点，退出全节点扣除抵押的 1% ，不需要审批和选举。（这里流通量指矿池以外可自由流通的代币，例如第一年 50 万，第二年是 55 万减去第一年的矿池收入，依次类推）
- Cosmos 的节点分为验证节点（全节点）、非验证全节点和轻节点，目前活跃验证节点 98 个，节点数最少 4 个，没有上限 。验证节点初始 100 个，10 年内每年递增 13% 直至稳定在 300 个。

### 交易

##### 交易手续费

- Polkadot 中继链和平行链都会收手续费，平行链还可以自定义手续费，但具体费率没有查到
- Mixin 交易免手续费，提现会超额收与交易所相当的手续费
- Cosmos 和以太坊类似，交易类型不同 Gas 不同，手续费越高交易就越有机会被打包执行

##### 交易最终确认时间

- Polkadot 在 10 - 12 秒内确认，参考[这里](https://wiki.polkadot.network/en/latest/glossary/#finality)
- Mixin 在 1 秒内确认，目前 15 个节点可在 300 毫秒内完成
- Cosmos 在 1 - 3 秒内确认，通常是 3 秒，跟验证器的数量有关，参考[这里](https://blog.cosmos.network/consensus-compare-tendermint-bft-vs-eos-dpos-46c5bca7204b)

##### 跨链转账

- 对于 Polkadot 来说，除了自己的中继链其他区块链都是平行链，所有原链上的代币都被转入多重签名控制的原链地址中并记录在中继链上，这样所有平行链的用户都在中继链这里得到了统一，交易经过一系列的验证和广播，最终实现了代币的转移。（这里是作者的理解，并没有找到确切的资料，网上文章关于这里的例子大多数只是强调验证和发送交易，并没有讲怎么收，需不需要调用智能合约，设计到转接桥的情况是不是不同）

- Mixin Kernel 本身不产生资产，链上只记录充值、提现和转账，所以内部转账也不需要监听原链和智能合约，并且支持单私钥管理多链资产，交易被打包后经过一系列的广播和验证，用户 A 增加 BTC 的转出记录，用户 B 增加 BTC 转入记录。用户充值后资产会自动转移至全节点管理的多签原链地址中，提现也从多签地址中转出。

- Cosmos Hub 会记录每个 Zone 所持有的代币总量，所有 Zone 内部转账和跨链转账都会通过并记录到 Cosmos Hub。跨链双方需要运行对方链的轻节点以便实时接收到对方的区块头信息，A 链用户先初始化  IBC 协议并用智能合约冻结相应的资产，然后把相应的证明通过 Cosmos Hub 发给 B 链用户，B 链用户收到后通过 A 链的轻节点检查核实，确认没问题后会新生成 1  TokenA 等价值 1 Wrapped Cosmos TokenA，这个 Wrapped Cosmos TokenA 可以在 Cosmos 内部流通，提现时被销毁。 — — Cosmos 流通的代币实际上是不被原链认可

> 跨链转账感觉有点伪命题，毕竟资产还是在原链上

### 主要特点

- Polkadot 支持直接调用其它链上的智能合约；基于 Substrate 可以很方便的构建分布式或去中心化系统，自动获得共识系统、P2P 网络、可运行智能合约的 WebAssembly 虚拟机等，从而专注在产品的核心业务逻辑上。

- Mixin 使用 CryptoNode 技术加强隐私使得转账交易无法被追踪；TPS 接近物理极限并且可以在 1 秒内完成交易最终确认；免费转账；单私钥管理多链资产；Domain Extension 支持智能合约调用，Dapp 跨链组合调用智能合约实现更强大的产品逻辑；对开发者非常友好，极大降低开发者的区块链应用开发学习成本，使用任何开发者熟悉的语言（Go、Java、Php 等）基于 REST API 结合区块链特点快速实现产品和业务。

- Cosmos 设计实现的 IBC 协议定义了一种通用的跨链协议标准，通过允许相互交易来打破区块链之间的障碍，从而构建一个更广泛的区块链互联网；Cosmos SDK 允许开发人员使用简单的模块化方案在 Cosmos 网络上设计自己的区块链，可以方便的添加治理、共识、网络等模块，甚至可以创建和发布属于自己的模块供其他链使用。

> Polkadot 强调的共享安全其他使用 Off-Chain 的跨链项目基本都具备，可能只是为了强调使用 Substrate 的便利性之一，因为代币一旦进入跨链区块链再转账就是内部转账，不会因为原链旷工增加或减少安全性。此外采用侧链技术 + PoS 也非常容易实现很高的 TPS ，这里就不再进行比较。

### 风险提醒

- 与 Polkadot 相关的 Web3 基金会与制订 Web 2.0 的 Web 标准的国际组织万维网联盟没什么关系，Web3 基金会实际上是由 Gavin Wood 组织成立，并且自己担任基金会主席，主要资助 Polkadot 和与其生态相关的部分项目；项目出现过严重的丢币事故；项目难度较大、开发周期较长

- Mixin 的国内外项目知名度不高；因第一款钱包产品使用手机号登录而被误批中心化；因受李笑来投资和推荐受到一些争议；节点不搞选举一定程度影响社区成员参与积极性

- Cosmos 团队曾经宣布过在 2017 年底上线主网，但实际上一直延期到 2019 年 3 月，多次跳票

### 总结

- Polkadot 最大优势是 Gavin Wood，因为他是前以太坊联合创始人 CTO；跨链调用智能合约非常具有想象力，但短期内除了做一点范例也实在没有更大的用途，原链本身就没有大规模的商业应用，跨链怎么可能出现大规模的应用，笔者认为此项技术真正应用还为时尚早；Substrate 区块链开发平台才是 Polkadot 最大的野心，降低了开发区块链的门槛，开发团队得以专注产品本身，与 Android 和 iOS 类似走平台路线，但是开发周期长、难度大。

- Mixin 最大优势也是创始人冯晓东，连续创业成绩都不错，项目迭代很快，测试网真实交易记录高达 2 亿多条，主网开发 1 年就已上线；支持隐私交易是一个非常重要且正确的方向；超高 TPS、亚秒级确认、零手续费可直接应用于大型商业项目；暂时不支持智能合约； Mixin 生态并不是以太坊、EOS 这样的去中心化的 Dapp 生态，而是 App + 去中心化钱包构成的新生态。

- Cosmos 的 SDK 区块链开发平台模块化组件非常厉害，围绕 SDK 本身就会有一个组件化生态，开发者能够真正参与到生态建设之中而不仅仅使用 SDK 提供好的组件，从生态接入数量多达八十多个便知；IBC 跨链协议为以后更广泛的跨链标准协议做出了示范，有整个区块链都有非常积极的意义。相比 Polkadot 和 Cosmos 的区块链开发平台，笔者更看好后者。

> 这三个项目与市面上大部分的区块链项目不同，并不是简单的 fork 一下、改一下共识、换一下参数、弄一个新的应用场景，都原创十足，更好的创新和竞争促使技术和行业发展，我们也能享受到更好的产品，我们一起拭目以待！

### 参考文章

- [【火币区块链产业专题报告】跨链篇（上）](https://www.jianshu.com/p/f2d2e83473fc)、 [跨链篇（下）](https://www.jianshu.com/p/b19b1f3cb9c7)
- [跨链技术的分析和思考](https://learnblockchain.cn/2019/03/23/blockchain_interoperability/)
- [另一个角度对比 Cosmos 与 Polkadot](http://www.coinvoice.cn/32393.html)
- [最完整的跨链专题报告（国脉区块链研究团队）](https://mp.weixin.qq.com/s/QmlLJ2i-ZgBAl9Bz80MP7g)
- [白话区块链 一文讲透 Cosmos 与 Polkadot](https://mp.weixin.qq.com/s/V5lphGLOkAecEnyYPvwT-Q)
- [Polkadot 和 Cosmos 的跨链生态之争](http://www.mimajike.com/2736/.html)
- [区块链的互操作性：Cosmos vs Polkadot](https://mp.weixin.qq.com/s/EiRzV-y-lakROiQQpAuVgg)
- [技术科普：互操作性对区块链的重要程度（以 Cosmos、Polkadot为例）](https://www.jinse.com/blockchain/351928.html)
- [Polkadot 官方 Wiki](https://wiki.polkadot.network) 、[Polkadot 官方 Medium](https://medium.com/polkadot-network/)
- [Polkadot 白皮书（中文翻译）](https://www.jianshu.com/p/1c463e205f55)
- [Polkadot：可扩展的异构多链系统（巴比特）](https://www.8btc.com/article/308888)
- [分分钟发链的背后，Substrate 技术框架能否开启跨链时代](https://www.8btc.com/article/296948)
- [Polkadot 创新 NPoS 共识下的 Staking 经济](https://www.8btc.com/article/394598)
- [Polkadot的链上治理模型（徐留成）](https://mp.weixin.qq.com/s/yyPaHsU7Nf7sUBVGIq1jbw)
- [Mixin 官方白皮书](https://mixin.one/assets/Mixin-Draft-2018-07-01.pdf)
- [Mixin 链接未来世界专题](https://www.jianshu.com/c/34802e95175a)
- [Mixin 白皮书（中文翻译）](https://www.jianshu.com/p/fa085b8bc9d1)
- [Mixin Network 是 PoS 版的比特币网络](https://www.jianshu.com/p/ed64085d5861)
- [Cosmos 白皮书](https://cosmos.network/resources/whitepaper)
- [Cosmos 官方 Medium](https://medium.com/coinmonks)
- [Cosmos Binance Research 项目深度报告](https://info.binance.com/en/research/ATOM-2019-4-28.html)
- [写在跨链项目Cosmos上线前夜](https://wallstreetcn.com/articles/3492765)
- [Cosmos 白皮书（翻译）](https://github.com/irisnet/translation/blob/master/Cosmos/Whitepaper_Chinese.md?from=singlemessage&isappinstalled=0#the-zones)
- [Cosmos SDK 官方中文资料](https://github.com/cosmos/cosmos-sdk/tree/master/docs/translations/cn)
- [Cosmos验证节点问题集—Part II](https://bihu.com/article/1236474)
- [深度挖掘 Cosmos 背后的技术实现](https://www.qklzhg.cn/news/77221/)
- [3分钟看懂 Cosmos Hub 的治理模型](https://bihu.com/people/971992)
