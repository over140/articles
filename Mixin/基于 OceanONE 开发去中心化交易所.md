重新开发一套新的交易所难度非常大，除了需要撮合引擎本身高性能无 bug 以外，还需要集成一大堆公链才能支持更多交易对；安全方面也不能马虎，交易所被黑、双花攻击、丢币的情况频发，对于有资源但是技术实力相对薄弱的团队确实很困难。集成靠谱的开源项目是个不错的选择，本文介绍基于 Ocean 撮合引擎开发一个去中心化交易所。

### 关于 Ocean 撮合引擎

- 团队靠谱
  Mixin 团队出品，必属精品，曾开发 [BigONE](https://big.one) 交易所，早些年开发的 Vitamio 播放 SDK 更是猎豹、微博、金山等多家知名企业使用，集成到数千个项目中。
- 去中心化
  用户资产和撮合引擎安全隔离，挂单成交后资产立即返回用户的钱包，速度等各方面体验匹敌传统中心化交易所
- 安全透明
  代码完全开源且通过了第三方机构审计，交易记录上链，可查可追溯
- 性能卓越
  24 小时最高完成 10,000,000 比真实交易，经得起量化交易团队批量交易
- 币种丰富
  支持 BTC、ETH、EOS、XMR 等 28 条主链超过 10 万种代币充值、提现和交易。
- 共享深度
  所有基于 Ocean 撮合引擎的交易所都将共享深度和流动性
- 独特优势
  所有基于 Mixin Network 的 Dapp 与交易所之间充值和提现都是免费、秒到；上币无须申请，默认全部自动支持；**交易手续费全额返还给开发者**

> 目前深度和流动性都不够，据说新版改完后会着手解决，接入其他交易所的深度

##### 架构和原理

Ocean 是基于 Mixin Network 使用 Go 语言实现的高性能撮合引擎，而 [OceanONE](https://ocean.one) 是基于 Mixin Network 的钱包 + 交易所前端 Dapp，通过转账来实现挂单、吃单和撤单，有效的隔离了用户资产同时交易上链提高透明度实现了去中心化的效果。

![Ocean 撮合引擎与其他 Dapp 的关系](https://wg.isdot.net/api/un/img?key=user-upload/12123326/d18eca4c17d779bc.png)

如图所有 Mixin Network 上的 Dapp 都可以直接给 Ocean 撮合引擎挂单，可以直接在 OceanONE 的源码上改改创建一个新的 Dapp 然后部署一下就是一个新的交易所了，显示什么交易对你说的算！

### 关于 Mixin Network

Mixin Network 是一个安全、免费、快速、加强隐私的去中心化支付网络，现已支持 13 条主链（BTC/ETH/EOS/DASH/XRP/XEM/SC/DOGE/BCH/LTC/ZEC/ETC/ZEN）超过 5.9 万种代币充值、提现和转账，是一条具备免费转账、实时到账的公链，可以简单理解为所有主流公链的闪电网络。

### 开发去中心化交易所

##### 注册开发者账号

App Store  或 Google Play 搜索下载 Mixin Messenger，扫码登录 https://developers.mixin.one（点右上角）。

> iOS 版本需要非中国区账号（国内被屏蔽了），也可以私信博主提供 Apple ID 邀请加入 TestFlight

##### 创建交易所 App

登录后点 Create New App 按提示创建。点 Click to generate a new session 生成 PIN、Session Id 、Pin Token、Private Key，这些都要记下来后面要用，服务器和浏览器都不会保存这些敏感信息（注意刷新网页再次点又会生成一个新的，会覆盖旧的）。
![Developers](https://wg.isdot.net/api/un/img?key=user-upload/12123326/248d94e2d2bcbcd2.png)

- The home uri
  一般用于 Mixin Messenger 小程序，打开小程序就是 Mixin Messenger 通过内置 WebView 打开这个链接作为入口。
- The OAuth redirect uri
  一般用于 Mixin Messenger 小程序，用于用户授权登录后 OAuth 回调

##### 方案一：基于 Mixin Messenger 的交易小程序

纯交易所前端，通过 Mixin Messenger 用户给撮合引擎挂单，但无法赚钱手续费。

![Mixcoin](https://wg.isdot.net/api/un/img?key=user-upload/12123326/c107e9856db67744.png)

- 开发前端交易界面
  常规的 html + css + js 开发，可直接基于 OceanONE 的开源前端代码来改

- OAuth 授权
  要访问用户的个人资料、资产列表等信息需要向 Mixin Messenger 申请授权。
  当检测到用户没有授权时可通过 https://mixin.one/oauth/authorize?client_id=b7347ca4-186e-4e54-9db6-755a4ab0b5d4&scope=PROFILE:READ+ASSETS:READ&response_type=code 向 Mixin Messenger 申请授权，参数 client_id 即开发者后台截图中的 User Id，参数 scope 参考文档 https://developers.mixin.one/api/beta-mixin-message/oauth-scopes/ 。
  授权成功后会回调开发者后台设置的 redirect uri ，并且返回一个 authorization code ，通过 https://api.mixin.one/oauth/token 验证成功后会返回 access_token ，这个很重要需要保存起来，据此可以判断当前用户是否已经授权过了。

- 访问授权用户
  访问授权用户的个人资料、资产列表等 API 都需要设置 Authorization Token， 直接用上面取到的 access_token 即可，参考代码 https://github.com/over140/mixcoin/blob/master/web/src/api/mixin.js
  
  ```
  GET -H "Authorization: Bearer ACCESS_TOKEN" https://api.mixin.one/me 
  {
  "data": {
    "type": "user",
    "user_id": "773e5e77-4107-45c2-b648-8fc722ed77f5",
    "name": "Team Mixin",
    "identity_number": "7000"
  }
  }
  ```

- 挂单交易
  由于 Ocean 的挂单是通过转账来实现的，每次挂单都需要生成一个支付链接https://mixin.one/pay?recipient=&asset=&amount=&memo=&trace= 唤起 Mixin Messenger 的支付界面完成转账，recipient 是收款人的 User Id，asset 是支付资产 id，amount 支付金额，trace 支付唯一编号 UUID，可以用来防止重复支付，每一笔交易都应该生成一个新的 trace，memo 参数用来存放挂单数据，参考 Ocean 在 Github 上的文档打包订单信息 https://github.com/MixinNetwork/ocean.one
  
  > 可以用轮询的方式根据 trace id 调用https://api.mixin.one/transfers/trace/trace_id 接口来检测是否已经完成支付，参考 js 代码：https://github.com/over140/mixcoin/blob/master/web/src/market/index.js 的 handleOrderCreate 方法。

> 取消订单也需要转账，可以让用户转账没有价值的币完成取消订单，比如 NXC、CNB 等也可以自己发行一个

- 源码
  交易小程序 Mixcoin 的全部源码在 https://github.com/over140/mixcoin ，在 Mixin Messenger 里搜索 7000101524 即可体验。

##### 方案二：独立的去中心化交易所

- 账号体系
  交易所的账号系统使用常规的手机号、邮箱、社交网络 SDK 登录都可以，还可以集成 Google 的二次验证，然后与 Mixin Network 账号关联：
  **单账户模型**：如果团队有能力替用户保管好 PIN 可以使用该方案，每一个交易所账号对应生成一个 Mixin Network 账号并关联，同时注册该账号为 Ocean 账号，将随机生成的 PIN 用开发者的私钥单独加密后存入交易所自己的数据库。这样就算被拖库只要代码服务器安全用户的资产还是安全的，但是无法处理可能存在的监守自盗问题。
  **双账户模型**：每一个交易所账号对应生成两个 Mixin Network 账号（A1 和 A2）并关联，A1 注册为 Ocean 账号并且将随机生成的 PIN 加密后存入交易所数据库由交易所管理，引导用户为 A2 设置支付密码（即 PIN 码）但不入库。 A2 为用户真正的钱包，所有订单通过 A1 账号中转发给撮合引擎，取消订单直接通过 A1 来完成，这样就算数据库和代码服务器都被攻破了用户的资产仍然安全的存在 Mixin Network 上而不被盗走。
  注册 Ocean 账号参考文档 List Orders 部分 https://github.com/MixinNetwork/ocean.one#list-orders

> 双账户模型还可以实现预充值的效果，需要一个资金池配合，比如充值 BTC 默认需要 12 个确认，大多数交易所只需要 1 个确认，充值就很慢，可以把 A1 的充值地址显示给用户，当监听到 A1 有资产充进来并且达到 1 个确认时就从资金池里直接把资产转给用户 A2，这样用户就能较快收到资产，等确认到账后把 A1 里的资产归还到资金池。

- 注册 Ocean 账户和取消订单的问题
  由于所有的操作都是通过转账来实现的，注册 Ocean 账户和取消订单就会有点问题，总不能花用户的资产来完成这两个操作，一个可行的办法就是发币来解决，并为每个新用户转一定数量的币，这个币不可交易不可提现，只用于这两个用途，每次消耗 0.00000001 即可。OceanONE 目前也是使用的这种方案，发行了 OOO 代币。

- 开发前端交易界面
  常规的 html + css + js 开发，可直接基于 OceanONE 的开源前端代码来改

- 挂单交易
  参考 [Mixin Network 转账 API](https://developers.mixin.one/api/alpha-mixin-network/transfer/) 根据 [Ocean 文档](https://github.com/MixinNetwork/ocean.one#list-orders)即可完成所有的操作。

- 源码
  OceanONE 全部源码 https://github.com/MixinNetwork/ocean.one/tree/master/example

> 监听充值、提现和其他 API 使用请参考 [Mixin 全币种钱包接入指南](https://steemit.com/cn/@over140/55jela-mixin)

### FAQ

- 为什么 OceanONE 看不到其他交易对 ？
  API支持所有交易对，但是网站只列出了部分

- 如何获取 asset id ？
  https://developers.mixin.one/api/alpha-mixin-network/read-assets/ 可以返回你资产列表，如果没有你的资产，你可以充值一点进来就有了

- 新的代币如何通过 Ocean 交易？
  Ocean 没有上币这一说，更没有上币费，直接将代币充值到 Mixin Network 即可交易 
