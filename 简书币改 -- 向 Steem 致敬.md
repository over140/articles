> 感谢 Steem，一位先行者。

以上是 Fountain 白皮书第一句话，要深度分析简书币改还得从 Steem 开始。Steem 是一个区块链公链项目，Steemit 是 Steem 上第一个去中心化内容社区应用，Steemit 开启了区块链内容激励的新时代，意义非凡。

考虑到本文读者会有一些非币圈用户，这里顺带做一点科普 ^ ^ ，由于收集整理资料时间仓促难免信息有误或者不全欢迎私信反馈！

### 什么是区块链（Blockchain）？
区块链一个公开的分布式账簿，账簿各数据记录之间使用密码学链接且只能增加，不能修改和删除 — — 即不可篡改，这个特性是通过去中心化网络来实现的，简单来说就是由一个人记账变成了多个人记账，这样其中一个人改了账簿而其他人没改很快就会被人发现。

**可见区块链是一种技术，能够促进公平提高透明度**

### 什么是加密货币（Cryptocurrency）？
依靠校验和密码技术来创建、发行和流通的电子货币。绝大部分加密货币没有政府信用背书（部分稳定币除外），这也是为什么很多人认为加密货币就是空气币的主要原因之一，我们看看经济学家怎么说：

> 一个东西作为货币，跟政府的信用背书没有什么关系。政府控制货币的历史很短，现在我们使用的货币由央行控制，人们就误以为它从来就这样，但它并非从来都是这样的，货币不需要一个强有力的信用背书。黄金作为最早的货币，或者其他贵金属作为货币的时候，也是没有政府做保证的。
> 比特币就是如此，它还原了货币的真正本质，就算没有政府信用背书，大家也信任它，因为比特币有自己的算法和技术。而且比特币已经进行了很多跨境交易。所以货币的五大职能（价值尺度、流通手段、贮藏手段、支付手段和世界货币）它都有，它是真正意义上的货币。  — —  以上出自著名经济学家王福重（经济学博士，北京大学博士后，中央财经大学经济学教授，中国世界经济学会理事）

如果你对加密货币也产生了兴趣，推荐重点研究比特币，去读读白皮书，比特币是世界上第一个，也是迄今为止最成功的区块链应用。

加密货币一般分 Coin 和 Token ，文章 [《多少人分得清 Coin 和 Token ?》](http://www.360doc.com/content/18/0526/09/31032795_757112924.shtml) 说得很好，但是不是本文重点，**为了便于说明后续会统称 Coin 和 Token 为代币**。

-------

### Steemit 简介
Steemit 是一个基于区块链的内容激励平台，内容以博客和社交媒体为主，用户通过参与贡献（发文章、评论、赞等）获得系统代币奖励，主要有以下特点：

- 经济激励：奖励每一个对社区有贡献的人，例如发文章、评论、赞等，越早加入并且贡献越多获得的系统奖励越多。
- 行为上链：所有用户行为都是公开、透明地被记录在区块链上。例如发文章、点赞、评论等，内容上链后后续可用于版权保护和内容溯源。
- 透明公平：代码开源、挖矿、奖惩机制、数据等公开透明可查询
- 社区自治：自发组成的团队对剽窃等不良行为进行治理、惩治、打击

##### 代币经济
![图片来源：chainnews](https://upload-images.jianshu.io/upload_images/647864-393e907dcaef186d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

- STEEM
可交易区块链代币 ，主要作用：
1、各大交易所买卖流通，主要是炒币（类似炒股）
2、Steemit Inc 开发团队定期售卖 STEEM 获取运营和开发资金
3、投资自己：后期加入 Steemit 的作者可以通过购买 Steem 兑换 SP 来提升自己的在社区的影响力

- STEEM POWER (SP)
用户权重（话语权/贡献值/股权/股份），主要作用：
1、SP 越多投票影响力越大，相应收益也会越高
2、SP 持有者获得 15% 增发分红
3、代理 SP（Delegated Steem Power）赚利息，把 SP 借给比如新用户，帮助他们更快发展
4、投票选举 21 位见证人
5、锁仓，当 STEEM 转成 SP 以后 STEEM 的流通量就减少了，相当于锁仓

- STEEM DOLLARS（SBD）
Steemit 内部市场流通稳定币，设计初衷是 1 : 1 锚定美元，主要作用：
1、保值，锚定美元，不管 STEEM 涨跌都是 1 SBD = 1 STEEM
2、消费，花钱推广（Promote）自己的文章，也可以在 Steemit Shop 买东西
3、利息，通过储蓄（Saving）赚取利息，类似银行活期利息

系统奖励分为 SBD 和 SP奖励，可以设置只收 SP。

##### Steemit 内容治理
- 踩（downvote）机制
如果文章被发现是抄袭、伪原创或者偏激言论和三言两语的毫无疑义的水贴可能被踩，当文章被人踩的太多或被权重高的人踩，收益为负的时候，文章就会变成灰色并且自动隐藏。
- 行为的速度限制，减少滥用
1、文章限制 64000 个字符，发文章间隔 5 分钟，发评论间隔 20 秒
2、投票权（Voting Power）：默认 100%，每次投票消耗 2%，每天线性恢复20%，为了保障投票效果最好控制在每天 10 次以内。如果你的权重（Steem Power）超过 500 投票时可以在 1% ~ 100% 之间更改：

![](https://upload-images.jianshu.io/upload_images/647864-284ff4f91395a6e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)
- 早鸟惩罚
为了防止机器人作弊，30 分钟内点赞的点赞者会有一定比例的收益交给原作者
- 声望系统
新用户默认 25 分，被踩或举报会降低声望，声望值低的人不能踩声望值高的人。
- 延迟奖励
投票会被延迟 24 小时后计算奖励，避免短时间内突击投票作弊

##### Steemit 数据统计
截止到目前总用户 [129 万](http://steemsql.com/status/)，日新增一百多，日活不足 5 万，月活不足 10 万，文章和评论也在持续下降：

![](https://upload-images.jianshu.io/upload_images/647864-9ecc1f7efcf41271.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

![](https://upload-images.jianshu.io/upload_images/647864-126cccd47e0b7491.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

以上数据来源：[Steem 统计数据 – 2019.07.14](https://steemit.com/cn/@arcange-cn/steem-statistics-20190714-cn)，以下是不同时间段最近一周的数据：

| 该时间最近一周 | 日新增 | 日发帖+评论 | 日投票
| :----: | :----: | :----: | :----: |
|  [2019-07-11](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-thursday-july-11-2019) | 164 | 53,585 | 546,575
|  [2019-04-11](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-thursday-april-11-2019) | 568 | 57,364 | 580,085
|  [2019-01-11](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-friday-january-11-2019) | 1,288 | 52,709 | 559,697
|  [2018-09-11](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-tuesday-september-11-2018) | 1,416 | 99,133 | 679,522
|  [2018-06-11](https://steempeak.com/steemit/@penguinpablo/weekly-steem-stats-report-monday-june-11-2018) | 2,240 | 154,735 | 708,912
|  [2018-01-11](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-thursday-january-11-2018) | 5,761 | 207,225 | 727,021
|  [2017-09-11](https://steempeak.com/steemit/@penguinpablo/weekly-steem-stats-report-monday-september-11-2017) | 1,808 | 98,857 | 347,167
|  [2017-06-12](https://steempeak.com/steemit/@penguinpablo/daily-steem-stats-report-june-12-2017) | 842 | 62,925 | 208,654

> 异常数据：2019-01-09 新增 4,108，2018-09-04 新增 5,670，可能有活动

再看一下 Steem 的排名和价格走势：

![](https://upload-images.jianshu.io/upload_images/647864-e35a99daed945e3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

> CMC 市值排名最高第 3，现在排名 80，市值最高 18 亿美金，现在市值仅剩 7 千万（2019-07-17）

##### Steemit 的困境
- 产品用户体验差
不愧是 BM 主导的产品，复杂难用，免费注册等 1 ~ 2 周，付费可立刻注册 https://signup.steemit.com 
- SBD 锚定机制有设计缺陷
SBD 在二级市场价格长期高于 1 美元或低于 1 美元且幅度较大
- 团队风险
CTO：BM（Dan Larimer） 只待了一年就离开去做新的项目了
2018 年 11 月 28 日 Steemit CEO Ned Scott 宣布裁员 70%
- 大鲸（big whale）问题
1‰的人手中掌握 76% Steem Power，富有者越来越富有，极大的削弱了平台的公平性，严重的中心化问题增加了见证人的选举被操纵的可能性。早期用户回报过大，而新用户没有名气、不充钱即使认真写收入很低，只好抱团互赞沦为权利的附庸。
- 币价影响过大
许多用户是因为可以挣钱才加入 Steemit，币价低赚不到钱自然不愿意继续贡献，导致热度变低币价更低陷入恶性循环
- 机器人泛滥
自动点赞帖子、评论机器人，自动跟随点赞机器人，相信也可以用机器学习来开发出自动写文章的机器人，照此下去离公地悲剧也不远了
- 内容分发问题
内容分发非常有限，在首页 New 下停留时间非常短，新写的文章每人看

**这是一场盛大的区块链内容激励实验，从统计数据和目前遇到的诸多问题来看 Steemit 已跌落神坛并持续恶化，用户数据与价格数据基本吻合，也许只有少数早期参与者确实赚到了钱，后续加入的资金和淘金者似乎并没有赚到钱甚至亏了钱，总有点 CX 的感觉**

-----

系统的了解 Steemit 能有助于我们理解简书币改的内容和方向，比如借钻功能就是这里的代理 SP，能量条机制等，简书币改现在遇到的很多问题其实都在 Steemit 上已经发生过，为后续分析和深度探讨提供了很好的参考。

查资料写文章不易，欢迎点赞，欢迎评论交流  

### 扩展阅读
以下文章如果不能点开说明要翻墙
- [扒一扒投资Steemit的SP点赞收益率有多大？](https://steemit.com/cn/@tumutanzi/how-much-money-can-you-earn-from-steem-power-curation-sttemit-sp)
- [Steem 项目评估：生态乏力裁员在即，代币体系存在设计缺陷]()
- [站在未来看现在：从现在的STEEM看未来的Fountain（上）](https://partiko.app/@tvb/steem-fountain)
- [Steem Wiki](https://www.steem.center)
- [Steem 中文社区集体创作: Steem Handbook](https://bookdown.org/baydap/steemh/aacontributors.html)
- [Steemit 深度研究总结](https://blog.csdn.net/kojhliang/article/details/80493338)
- [数字货币入门简介](https://www.jianshu.com/p/2523475ad0a3)
- [给区块链改变生产关系泼点冷水](https://www.jianshu.com/p/b505ce495e28)