# 拍卖调研文档

- [拍卖调研文档](#拍卖调研文档)
- [参考](#参考)
- [拍卖定义](#拍卖定义)
- [拍卖术语](#拍卖术语)
    - [保留价](#保留价)
    - [拍卖人](#拍卖人)
    - [拍卖师](#拍卖师)
    - [委托人](#委托人)
    - [竞买人](#竞买人)
    - [买受人](#买受人)
    - [图录](#图录)
- [拍卖方式](#拍卖方式)
  - [英格兰式 英国式](#英格兰式-英国式)
  - [荷兰式](#荷兰式)
  - [密封递价式](#密封递价式)
  - [最高价得标拍卖法](#最高价得标拍卖法)
  - [标准增量式](#标准增量式)
  - [维克瑞式](#维克瑞式)
  - [速胜式](#速胜式)
  - [反向拍卖](#反向拍卖)
  - [定向拍卖](#定向拍卖)
  - [共有价值拍卖](#共有价值拍卖)
  - [组合拍卖](#组合拍卖)
  - [司法拍卖](#司法拍卖)
  - [多轮拍卖（Simultaneous Multiple Round Auction）](#多轮拍卖simultaneous-multiple-round-auction)
  - [双重拍卖（双向拍卖）（Double Auction）](#双重拍卖双向拍卖double-auction)
- [竞价模式与交易方式](#竞价模式与交易方式)
- [常见拍卖规则](#常见拍卖规则)
    - [一、针对委托人](#一针对委托人)
    - [二、针对拍卖人](#二针对拍卖人)
    - [三、针对竞买人](#三针对竞买人)
    - [四、针对买受人](#四针对买受人)
- [**拍卖流程**](#拍卖流程)
    - [一 接受拍卖委托](#一-接受拍卖委托)
    - [二 收取委托人保证金](#二-收取委托人保证金)
    - [三 发布拍卖公告、制作拍卖文件](#三-发布拍卖公告制作拍卖文件)
    - [四 拍卖咨询登记](#四-拍卖咨询登记)
    - [五 布置拍卖会场](#五-布置拍卖会场)
    - [六 实施拍卖](#六-实施拍卖)
    - [七 整理拍卖全部资料并归档保存](#七-整理拍卖全部资料并归档保存)
- [司法拍卖](#司法拍卖-1)
  - [司法竞拍流程](#司法竞拍流程)
    - [1.阅读公告](#1阅读公告)
    - [2.实地看样（非强制）](#2实地看样非强制)
    - [3.交保证金](#3交保证金)
    - [4.出价竞拍](#4出价竞拍)
    - [5.竞拍成功](#5竞拍成功)
    - [6.办理交割](#6办理交割)
  - [网络司法拍卖](#网络司法拍卖)
- [广告竞价策略：GFP，GSP，VCG](#广告竞价策略gfpgspvcg)
  - [广义第一价格（Generalized First Price,GFP)](#广义第一价格generalized-first-pricegfp)
  - [广义第二价格（Generalized Second Price , GSP)](#广义第二价格generalized-second-price--gsp)
  - [（Vickrey-Clarke-Groves，VCG）](#vickrey-clarke-grovesvcg)
- [开源项目](#开源项目)



# 参考

[拍卖（公开竞价的买卖方式）_百度百科](https://baike.baidu.com/item/拍卖/81152#6)

[拍卖 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/拍卖)

# 拍卖定义

《中华人民共和国拍卖法》定义：“以公开竞价的方式，将特定的物品或财产权利转让给最高应价者的买卖方式”。

# 拍卖术语

### 保留价

这是指物主愿意将物品让出的最低价格，这一价格一般是物主与拍卖行协商产生的，价格也是对外保密的。大多数时候它都会比开价略高，但也会和开价一样或比开价低。**如果拍卖的最后叫价没有达到保留价，物主就有权利不将该物品卖出；但如果最后叫价比保留价高出许多，物主则可以从中获利。**

起拍价是低于底价的，如没人应拍或虽有人叫价，但最终叫价低于底价，则所拍物品不成交。

### 拍卖人

是指依法设立的从事拍卖活动的企业法人。

### 拍卖师

拍卖活动由拍卖师主持。

### 委托人

是指委托拍卖人拍卖物品或者财产权利的公民、法人或者其他组织。

### 竞买人

是指参加竞购拍卖标的的公民、法人或者其他组织。

### 买受人

是指以最高应价购得拍卖标的的竞买人。

### 图录

拍卖行在征集拍品后，会收集该拍品的有关资料，然后编号印成图录。

# 拍卖方式

## 英格兰式 英国式

也称“增价拍卖”或“低估价拍卖”，最常见的拍卖方式。是指在拍卖过程中，拍卖人宣布拍卖标的的起叫价及最低增幅，竞买人以起叫价为起点，由低至高竞相应价，最后以最高竞价者以三次报价无人应价后，响槌成交。但成交价不得低于保留价。

竞标者可多次重复提高出价，常见于拍卖场苏富比拍卖会，台湾的夜市竞标皆以此法拍卖。

## 荷兰式

也称“降价拍卖”或“高估价拍卖”。是指在拍卖过程中，拍卖人宣布拍卖标的的起拍价及降幅，并依次叫价，第一位**应价**人响槌成交。但成交价不得低于保留价。

英格兰式与荷兰式相结合的拍卖方式。是指在拍卖过程中，拍卖人宣布起拍价后及最低增幅，由竞买人竞相应价，拍卖人依次升高叫价，以最高应价者竞得。若无人应价则转为拍卖人依次降低叫价及降幅，并依次叫价，以第一位应价者竞得。但成交价不得低于保留价。

创于荷兰的郁金香拍卖场而得名，除荷兰外，台湾的蔬果、鱼肉批发市场亦是以此种方式拍卖，常应用于有一定数量之商品拍卖时。

荷兰式拍卖的好处是，价格从高往低，一旦落入消费者心理价位区间内的最上限，他就会购买。

## 密封递价式

又称**招标式拍卖**。由买主在规定的时间内将密封的报价单（也称标书）递交拍卖人，由拍卖人选择买主。这种拍卖方式，和上述两种方式相比较，有以下两个特点：一是除价格条件外，还可能有其他交易条件需要考虑：二是可以采取公开开标方式，也可以采取不公开开标方式。拍卖大型设施或数量较大的库存物资或政府罚没物资时，可能采用这种方式。

在暗拍中，因为参与者完全不知道别人的出价，于是都只好报出自己心理价位的最高报价，来提高成交机会。上海的汽车牌照，就是最典型的暗拍。

密封拍卖可分为一级密封拍卖和二级密封拍卖。

一级密封拍卖也称为密封递价最高价拍卖，即在密封递价过程中，出价最高的竞买人中标。如果拍卖的是多件相同物品，出价低于前一个的竞买人购得剩余的拍卖品。

二级密封拍卖也称为密封递价次高价拍卖，其递价过程与一及密封拍卖类似，只是出价最高的竞买人是按照出价第二高的竞买人所出的价格都按其预告价出价，降低了竞买人串通的可能性，获胜者不必按照最高价付款，从而使所有的竞买人都想以比其一级密封拍卖中高一些的价格出价。

## 最高价得标拍卖法

密封投标金额，投标者只能出价一次，开标时最高价者得标并依价付款，广泛应用在土地、公用工程的竞标上。

## 标准增量式

这是一种拍卖标的数量远大于单个竞买人的需求量而采取的一种拍卖方式（此拍卖方式非常适合大宗积压物资的拍卖活动）。卖方为拍卖标的设计一个需求量与成交价格的关系曲线。竞买人提交所需标的的数量之后，如果接受卖方根据他的数量而报出的成交价即可成为买受人。

## 维克瑞式

维克瑞拍卖，也称为第二价格密封拍卖。这种拍卖方式与首价密封拍卖基本相同，区别仅在于胜出者需要支付的价格是第二高的报价，而不是他自己的报价，竞标价者想出价几次都行。这与易趣网所使用的代理人竞价系统相似，在这个系统中，胜出者需要支付第二高的报价，再加上一个报价的增额（如10%）。此种拍卖法会有垄断商品（故意喊巨额的价钱，使其他竞标者无法得标）的行为发生，所以是最不常采用的。

如果出价最高者赢得拍卖，却只需要支付第二高价，那就会激发每个人都出高于自己心理价位的更高价。**到最后，真正的成交价，就会远高于预期。**

谷歌，百度，阿里的竞价排名广告，用的都是维克瑞拍卖。

## 速胜式

这是**增价式拍卖**的一种变体。拍卖标的物的竞价也是按照竞价阶梯由低到高、依次递增，不同的是，当某个竞买人的出价达到（大于或等于）保留价时，拍卖结束，此竞买人成为[买受人](https://baike.baidu.com/item/买受人)。

## 反向拍卖

反向拍卖也叫拍买，常用于政府采购、工程采购等。由采购方提供希望得到的产品的信息、需要服务的要求和可以承受的价格定位，由卖家之间以竞争方式决定最终产品提供商和服务供应商，从而使采购方以最优的性能价格比实现购买。

## 定向拍卖

这是一种为特定的拍卖标的物而设计的拍卖方式，有意竞买者必须符合卖家所提出的相关条件，才可成为竞买人参与竞价。

## 共有价值拍卖

一个被拍卖的商品对于所有的竞标者而言价值是相同的，但是竞标者在竞标时不知道该商品的价值。典型的例子包括石油开采权。

## 组合拍卖

组合拍卖是拍卖的一种，于1982年提出，它与传统拍卖不同，是一种竞价人可以对多种商品的组合进行竞价的拍卖方式。它适用于买方对商品价值衡量呈现非加性的情况。与传统的拍卖方式相比，组合拍卖在分配多种商品时效率更高。

这种拍卖方式的目标为多种商品。由买方写下多种商品的组合与对该组合所出的价格，或由卖方提供不同的组合，由买方对卖方提供的组合出价。这种拍卖方式比单一物品拍卖有效地提高组合物品的价值。

## 司法拍卖

司法拍卖是人民法院在民事案件强制执行程序中，按程序自行进行或委托拍卖公司公开处理债务人的财产，以清偿债权人债权的工作。

## 多轮拍卖（Simultaneous Multiple Round Auction）

在美国FCC的无线电频谱拍卖中，运营商同时获得相邻地区和相近频谱有助于降低地运营成本。因此，赢得单个地区或者单个频谱许可证的价值还受其在其他地区和其他频谱竞争结果的影响。未能获得理想的地区或者频谱组合的运营商将私下与其他运营商进行合谋或者市后交易，催生庞大的二手市场，可见频谱资源并未在拍卖中得到有效的分配。

针对此问题，在美国FCC拍卖无线电频谱许可证的设计中，米尔格罗姆和威尔逊设计出一种全新的拍卖方式，同时多轮拍卖 （Simultaneous Multiple Round Auction），将所有的频段同时放出，价格由低到高进行多轮报价。每一轮中，竞拍者可以同时竞拍一个或者多个频段，从而解决了物品间相互关联带来的问题。

## 双重拍卖（双向拍卖）（Double Auction）

双重拍卖指买卖双方同时向拍卖人提出竞价和要价，由拍卖人确定成交价格的一种拍卖程序；一些**股票**市场使用的公开叫价制度就是一个没有人在买卖双方之间进行调解的双重拍卖的例子。

双向拍卖指只要一方中有人接受另一方的叫价，两者便可以达成交易，每一次交易一个商品。然后再开始新一轮的叫价，可以有多个交易期，交易价格总是介于初始出价和初始要价之间。在整个交易过程中，价格信息是公开的。

该方式是买方和卖方同时递交价格和数量来出价。在网上双重拍卖中，买方和卖方出价是通过软件代理竞价系统进行的。拍卖开始前，买方向软件代理竞价系统提交最低出价和出价增量，卖方向软件代理竞价系统提交最高要价和要价减量。网上拍卖信息系统把卖方的要约和买方的要约进行匹配，直到要约提出的所有出售数量都卖给了买方。双重拍卖只对那些事先知道质量的物品有效。

# 竞价模式与交易方式

目前国内外的拍卖网站，其竞价模式实际上只有两种，即正向竞价和逆向竞价

其交易方式则有三种：竞价拍卖、竞价拍买和集体议价。

# 常见拍卖规则

### 一、针对委托人

1、委托人不得参与竞拍或委托他人竞拍自己委托的拍品

### 二、针对拍卖人

1、拍卖人的工作人员不得参与竞拍或委托他人竞拍标的

### 三、针对竞买人

1、竞买人可在拍卖前对标的进行查验。拍卖标的以拍卖当天的情况为准，拍卖人所提供的图片、文字信息等资料仅供竞买人参考。

2、竞买人办理竞买手续，须交保证金xxxx元（根据自己拍卖行情况制定），领取竞买号牌。

3、在拍卖会上竞买人一经应价不的撤回。若有更高应价，其应价即丧失约束力。

4、竞买人不得影响拍卖会场的纪律。

5、本场拍卖会采用增价（或降价）的形式进行拍卖。竞买人根据拍卖师的竞价阶梯进行竞价。拍卖师有权根据场上的竞价情况对竞价阶梯进行调整。

6、竞买人的最高应价经拍卖师落槌的方式确认后，拍卖成交。最高应价者须当场签署成交确认书。

### 四、针对买受人

1、标的成交后，买受人须支付成交价款及xx%的拍卖佣金（佣金比例根据自己拍卖行情况制定）

2、成交价款及拍卖佣金需在xx个工作日内到账（根据自己拍卖行情况制定）

3、支付完所有款项后，买受人需在XX个工作日内提取拍卖标的，未按照约定提取拍卖标的的，应当支付由此产生的保管费用。

4、买受人在拍卖成交后拒绝支付成交价款及拍卖佣金拍卖行将按照《拍卖法》第三十九条的规定进行处理。

# **拍卖流程**

### 一 接受拍卖委托

（一）委托人需提供资料，1.拍卖标的清单及瑕疵说明 。 2.拍卖标的。比如：评估报告； 拍卖标的清单；拍卖标的处置权证明。3.拍卖标的瑕疵说明 ⑴对标的物现有状况相关问题及瑕疵的说明； ⑵对标的的资产评估报告以外的事项说明(包括或有事项)。4.涉及股权拍卖的委托人除提供上述资料外还应提供被转股企业的相关资料：

（二）拍卖人核查拍卖标的处置权及相关事宜： 1.对委托人及代理人的资格身份审查； 2.拍卖标的权属的审查； 3.审查评估报告及鉴定结论的真实性（实地调查或函调）； 4.拍卖标的存在的问题及瑕疵； 5.涉及股权拍卖的应审查： ⑴被拍卖股权企业的股东构成和股本结构； ⑵股权的类型及币种； ⑶向被转股企业的主管部门备案，为拍卖成交股权转移做前期准备。

（三）拍卖人与委托人签订拍卖合同。

### 二 收取委托人保证金

委托人在签订委托拍卖合同时，拍卖人必须收取委托保证金，存入拍卖人设立的拍卖专户或在拍卖人监控下存入由委托人与拍卖人共同设定账户。拍卖人出据收取委托保证金的收据。

### 三 发布拍卖公告、制作拍卖文件

（一）拍卖人草拟拍卖公告文本。

（二）征得委托人书面确认后，在委托人指定或国家认可的媒体上发布拍卖公告(国家有特殊规定的按规定办理)。

（三）拍卖公告发布时间为接受委托后三个工作日或以委托人确定时间为准(因媒体原因导致发布时间变化除外)。

（四）制作拍卖文件 1.竞买须知; 2.标的情况介绍(标的目录); 3.标的相关证件，影像资料等; 4.标的相关瑕疵说明。

### 四 拍卖咨询登记

（一）自媒体发布拍卖公告之日起，拍卖人设专人负责接待咨询登记工作;

（二）咨询介绍的内容仅限于拍卖文件资料及委托人提供的拍卖标的资料;

（三）竞买人登记：1.提供竞买人资料并盖章签字 ⑴企业营业执照原件; ⑵企业法人或代理人身份证明; ⑶企业法定代表人授权代理人的授权委托书; ⑷自然人身份证原件的复印件、银行资信证明; ⑸自然人授权代理人的授权委托书、代理人的身份证明; ⑹竞买专营、专卖物品，须提供专营、专卖资质证明文件; ⑺境外公司注册文件、银行资信证明和法定代表人身份证明; ⑻境外自然人身份证明、银行资信证明; ⑼境外竞买人委托代理竞标的应提供经境外公证后的授权书及代理人的身份证明。2.审查竞买人资格 3.签定竞买协议 4.确定竞买号牌 5.委托代理人参加竞买的须提交竞买人与竞买代理人签定的《授权委托书》

（四）竞买人在签定竞买协议时拍卖人必须收取竞买保证金，存入拍卖人设立的拍卖专户或在拍卖人监控下存入由竞买人与拍卖人共同设定账户。拍卖人出据收取竞买保证金的收据。

（五）境外竞买人开立临时账户所需资料： 1.外国投资者本人或其委托人提交的书面申请(投资者基本情况、拟开户银行及开户金额、账户资金用途等情况)； 2.境外法人当地注册登记证明或境外自然人身份证明； 3.公司名称预先核准通知书或有关部门的证明文件； 4.自然人身份证原件的复印件、银行资信证明； 5.境外投资者委托境内自然人或法人申请开户应提供依法办理涉外公证的授权委托书； 6.外汇管理局要求的其他材料。

### 五 布置拍卖会场

（一）会场布置突出标的专场的特点；

（二）会场设定拍卖台、现场记录、现场见证或公证、现场监督、竞买人和来宾等专门席位；

（三）会场灯光明亮柔和，环境舒适；

（四）会场音响效果良好。

### 六 实施拍卖

（一）拍卖会前2小时拍卖工作人员到场按分工进入角色，核准登记办理竞买人入场手续；

（二）按拍卖公告公布的时间、地点，开始公开拍卖；

（三）拍卖会主持人宣读会场注意事项及拍卖须知；

（四）拍卖师主持拍卖竞价。竞价前清点竞买人，介绍监拍人，由委托人出示保留价，公布举报电话；

（五）记录拍卖过程、进行现场摄录像，保证拍卖过程真实合法；

（六）竞价原则：价高者得。 落槌成交后由见证员宣读现场见证书或由公证员宣读现场公证书，由买受人与拍卖人签定《拍卖成交确认书》；

（七）在拍卖人监督下，买受人、委托人及拍卖人签定拍卖标的转移协议；

（八）拍卖人向买受人和委托人分别收取拍卖佣金；

（九）拍卖会结束。

### 七 整理拍卖全部资料并归档保存

1 拍卖人向买受人与委托人提供有效的成交证明和拍卖资料，由买受人与委托人自行向有关行政管理机关办理相关标的转移手续。

2 委托人与买受人履行标的交割及价款交付手续，须向拍卖人交付相关证明文件。拍卖人审验无误后结算双方的保证金。

3 整理拍卖资料归入拍卖档案。

拍卖业务的一般程序可分为三个阶段：

**准备阶段**

货主把货物运到拍卖地点→委托拍卖行进行挑选和分批→拍卖行编印目录并招揽买主。参加拍卖的买主可以在规定的时间内到仓库查看货物→了解商品品质→拟定自己的出价标准，做好拍卖前的准备工作。拍卖行一般还提供各种书面资料，进行宣传以扩大影响。

**正式拍卖**

正式拍卖是在规定的时间和地点，按照拍卖目录规定的次序逐笔喊价成交。拍卖过程中，买主在正式拍卖的每一次叫价，都相当于一项发盘，当另一竞买者报出更高价格时，该发盘即行失效。拍卖主持人以击槌的方式代表卖主表示接受后，交易即告达成.

**成交交货**

拍卖成交后，买主即在成交确认书上签字，拍卖行分别向委托人和买主收取一定比例的佣金，佣金一般不超过成交价的5%。买主通常以现汇支付货款，并在规定的期限内按仓库交货条件到指定仓库提货。由于拍卖前买主可事先看货，所以，事后的索赔现象较少。但如果货物确有瑕疵，或拍卖人、委托人不能保证其真伪的，必须事先声明，否则，拍卖人要负担保责任。

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fccdf265e-b88e-4967-b564-da9f5ec9c4f5%2FUntitled.png?table=block&id=d1a4e42e-0384-4fb9-8172-b984d6960626&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2)![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2b9cabbc-b20b-4115-9d69-38da07ec2fb2%2FUntitled.png?table=block&id=b75d59e6-8675-447f-9b15-40d53c98bbdd&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2)

# 司法拍卖

## 司法竞拍流程

### 1.阅读公告

### 2.实地看样（非强制）

### 3.交保证金

### 4.出价竞拍

### 5.竞拍成功

### 6.办理交割

## 网络司法拍卖

据最高人民法院最新通知，网络司法拍卖从 2017 年 9 月16 日开始，变卖期为 60 天，如有竞买人在 60 天内变卖期中的任一时间出价，则变卖自动进入到 24 小时竞价倒计时；24 小时竞价周期内，其他报名用户可加价参与竞买，竞价结束前 5 分钟内如有人出价，则系统自动向后延时 5 分钟（循环往复至最后 5 分钟内无人出价）。

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa650c9bd-5369-4280-b320-5f54bc46f01e%2FUntitled.png?table=block&id=1ac6bf20-832d-4bbb-a7b7-72ceaf871537&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2 "淘宝司法拍卖流程")

<center>淘宝司法拍卖流程</center>

竞拍的保证金金额不得超过起拍价的 20%，如拍卖成交后悔拍的，保证金将不予退还；在网络司法拍卖竞价期间无人机出价，当次拍卖流拍的，应当在 30 日内在同一网络司法拍卖平台再次拍卖，再次拍卖的起拍价降价幅度，不得超过前次起拍价的 20%。

2016 年 12 月，最高人民法院公布了 5 家网络司法拍卖平台的名单，其中分别为 淘宝网、京东网、人民法院诉讼资产网、公拍网、中国拍卖行业协会网。

最高人民法院今年还对网络司法变卖的规则进行了调整，从 2017 年 9 月 16 日起，网络司法拍卖的规则有多处变更，其中最重要的一条是：竞买人需要缴纳等同于标的物变卖价全款金额的变卖预缴款，才能获得参拍资格。区别于此前缴纳一定比例的保证金就能够参拍。就是说，如果你要参与竞拍一套起拍价为 20 万元的房子，并且法院是在 2017 年9 月 16 日后才发布拍卖公告的，那么你除了要缴纳不超过 20% 的保证金，还需要提前交 20 万元作为预缴款。

# 广告竞价策略：GFP，GSP，VCG

## 广义第一价格（Generalized First Price,GFP)

广义第一价格就是按照出价去计费，价格高者排在前面，它的优势就是简单，收入可保证，但是稳定性较差。各个广告主为了获得最佳收益，可以通过频繁修改投放价格而获得。举例来说，一个广告主为了获得展现，它会不断的的增加价格，在获得展现后，它又会开始不断的减少价格而降低成本，这种竞争是相对武断的，而且很容易知晓竞争对手的出价。另外，当出价最高广告主停止投放后，容易对广告平台收入产生较大的波动。在2002年之前，所有的搜索引擎都是第一出价法则。

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5213b06f-4cee-421c-89a8-2383836ff090%2FUntitled.png?table=block&id=7217b418-162d-4f40-ae0e-5c985edef3cc&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2)

## 广义第二价格（Generalized Second Price , GSP)

其实广义第一价格没有那么坏，对于大部分广告平台来说，至少收入在一定程度来说是最大的。那么如何更加吸引更多的广告主的投放？并且降低广告主投放的成本，减少优化的成本呢？谷歌在2002年，将广义第二价格的方式引入搜索引擎，基本原理就是按照下一位的出价，来实际扣费，为了鼓励广告主提高素材，广告点击率。实际计费的公式变成了

收费=下一位价格*(下一位质量分／本位质量分）＋０.０１

![https://pic1.zhimg.com/80/9af7515578089830689ad1177661175c_720w.jpg](https://pic1.zhimg.com/80/9af7515578089830689ad1177661175c_720w.jpg)

## （Vickrey-Clarke-Groves，VCG）

还有一种计费方法叫做VCG，名字来源于三个牛人的名字，其中最有名的 Vickrey是一个出生在加拿大的经济学家，1996年获得诺贝尔经济学奖，他在竞拍理论上有突出的贡献，他提出了第二价格的竞拍方法，广泛用于各种经济活动。VCG是一种比第二价格还要晦涩的一种方法，它的基本原理是计算竞价者赢得广告位后，给整个竞价收入带来的收益损失，理论上这种损失就是竞价获胜者应该支付的费用。

![https://pic1.zhimg.com/80/95a4e86cc543606059af5911d098ad64_720w.jpg](https://pic1.zhimg.com/80/95a4e86cc543606059af5911d098ad64_720w.jpg)

# 开源项目

1.盲拍、公开拍卖

[Hsiang-xxs/Auction](https://github.com/Hsiang-xxs/Auction)

2.英式拍卖

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F699a30c3-bd76-43b4-ba87-b9d9df75e132%2FUntitled.png?table=block&id=21c0ad80-7216-4068-be7f-b078ff5f48e1&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2)

[timxor/english-auction](https://github.com/timxor/english-auction/blob/main/english_auction.sol)

3.关于NFT的固定价格订单，荷兰拍卖订单，英式拍卖订单

[TheGreatHB/NFTEX](https://github.com/TheGreatHB/NFTEX/blob/main/contracts/NFTEX.sol)

4.荷兰拍卖

[upandey3/Ethereum-SmartContract](https://github.com/upandey3/Ethereum-SmartContract/blob/master/contracts/DutchAuction.sol)

5.NFT英式拍卖

[iNDicat0r/mastering-ethereum-auction-dapp](https://github.com/iNDicat0r/mastering-ethereum-auction-dapp/blob/master/README.md#decentralized-auction-application-on-ethereum)

6.NFT荷兰拍卖

[ssteiger/Ethereum-NFT-Store-with-Dutch-Auctions](https://github.com/ssteiger/Ethereum-NFT-Store-with-Dutch-Auctions)

7.维克瑞拍卖

[Nangos/vickrey-on-ethereum-frontend](https://github.com/Nangos/vickrey-on-ethereum-frontend)

8.维克瑞拍卖

[Nangos/vickrey-on-ethereum-frontend](https://github.com/Nangos/vickrey-on-ethereum-frontend/blob/main/nft-vickrey.sol)

9.维克瑞拍卖

[york-yang-me/EShop](https://github.com/york-yang-me/EShop)

10.荷兰拍卖

![img](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F77754735-ba23-4fd0-b8f3-cb2ccc9dd129%2FUntitled.png?table=block&id=6b93ee17-e8d5-4e8c-97a0-170d812014c1&spaceId=60ca1edb-2635-4407-9e59-c9b30fd5cea5&width=3840&userId=5e299d3b-e72c-468b-8871-3199bbe4f257&cache=v2)

[matthew-wan/Solidity-Dutch-Auction](https://github.com/matthew-wan/Solidity-Dutch-Auction)