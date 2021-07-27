- [导读·万维网](#导读万维网)
  - [HTML（HyperText Markup Language）：超文本标记语言](#htmlhypertext-markup-language超文本标记语言)
  - [URI（Uniform Resource Identifier）：统一资源标志符](#uriuniform-resource-identifier统一资源标志符)
  - [HTTP（HyperText Transfer Protocol）：超文本传输协议](#httphypertext-transfer-protocol超文本传输协议)
- [NFT vs FT](#nft-vs-ft)
- [NFT的技术规范](#nft的技术规范)
  - [ERC-721](#erc-721)
    - [tokenId](#tokenid)
    - [name](#name)
    - [symbol](#symbol)
    - [uri](#uri)
  - [ERC-1155](#erc-1155)
    - [单个合约能同时管理 FT 和 NFT](#单个合约能同时管理-ft-和-nft)
    - [支持批量转账](#支持批量转账)
    - [对uri所链接到的外部JSON文档的格式做了一些小改动](#对uri所链接到的外部json文档的格式做了一些小改动)
- [NFT的应用场景](#nft的应用场景)
  - [实体经济](#实体经济)
    - [商品溯源](#商品溯源)
    - [知识产权](#知识产权)
    - [证据存证](#证据存证)
    - [电子票据](#电子票据)
    - [电子证件](#电子证件)
  - [虚拟及金融资产](#虚拟及金融资产)
    - [数字收藏品](#数字收藏品)
    - [游戏资产](#游戏资产)
    - [虚拟世界](#虚拟世界)
    - [加密艺术品](#加密艺术品)
    - [金融](#金融)
    - [其他](#其他)
  
# 导读·万维网

回顾信息互联网的几十年的发展历程，万维网（World Wide Web，WWW）是其中最为重要的进展之一。

当提及信息互联网时，多指万维网。

经常说的Web1.0、Web2.0、Web3.0，多指万维网。

万维网最重要的三项技术规范：
## HTML（HyperText Markup Language）：超文本标记语言
超文本标记语言HTML用于将信息规范化地表示出来
## URI（Uniform Resource Identifier）：统一资源标志符
统一资源标志符URI用于标识信息的名称和位置
## HTTP（HyperText Transfer Protocol）：超文本传输协议
超文本传输协议HTTP用于传输信息

**NFT会成为价值互联网中的HTML，起到将价值规范化地表示出来的作用。**        
&nbsp;

# NFT vs FT

价值，说通俗点就是资产。区块链里表示资产就是 Token。

Token 有2种：Fungible Token（同质化通证，FT） 和 Non-fungible Token（非同质化通证，NFT）。

其中FT最广泛的技术规范是 ERC-20，NFT最广泛的技术规范是ERC-721

| FT   | NFT |
| ---- | ---- |
| 每个Token是同质化的，没有ID进行标识 | 每个Token是同质化的，有唯一的ID |
| 每个Token是可分割的，数量可以是小数 | 每个Token是不可分割的，数量必须是整数 |
| 无外部信息关联的属性 | 有可以与外部信息关联的URI属性 |

基于上面FT和NFT的区别，我们发现NFT技术在实体资产的数字化上更有优势：

* 非同质化：你的电脑和其他人的电脑可能是用一个型号，但是它们的序列号不同，它们安装的软件不同，它们存储的文件也不同...
* 不可分割：你的书籍不可能是0.5本、你的手机也不可能是0.25只...
* 有外部信息关联方式：每个NFT有个属性可以与外部URI关联，这个URI可以链接到你的资产的一些详细信息，如生产厂商、生产日期、外观图片...

除了实体资产，虚拟资产用NFT来表示也更加方便，因为虚拟资产本身的形式就是数字化的，如一个游戏道具，可以通过URI关联到一个NFT。

大部分金融资产更适合用 FT 的方式来表示，因为很多金融资产都是同质化的，如同一家公司的同类型股票，这1股和另1股是一样的。当然像保险单这样的因人而异的金融资产还是适合用NFT来表示。

物理世界的资产其实本质上都是非同质化的。就算是流水线上生产出来的标准化产品，不同产品之间本来就是有细微差异的。而在产品发售由不同客户购买后，因为不同客户对产品不同的使用方式、使用强度，最后这些二手产品之间的非同质化程度会进一步增加。

NFT和FT是互补的，NFT可能会是价值互联网的 HTML，而FT可能会是价值互联网的 JSON/XML 。

# NFT的技术规范

NFT目前主要的技术规范是以太坊上的ERC-721和ERC-1155。

在ERC-721的规范提出后又涌现了很多新的NFT的规范，如ERC-1155。除此之外，还有ERC-1523（保险单NFT）、ERC-998（可组合的NFT）、EIP-1948（可变信息的NFT）、EIP-2981（NFT版税）等。ERC-721和ERC-1155目前在EIP中的状态为final，而其他几个都为draft。

ERC-721和ERC-1155都有基本的**资产转账**、**资产授权**、**查询资产所属用户**、**查询用户所拥有资产**的方法。

## ERC-721
ERC-721规范的NFT一般具有以下属性：
### tokenId
在合约内唯一的 NFT ID，在NFT的生命周期中不可改变（要实现全链唯一的必须用(contractAddr, tokenId)组成的元组）
### name
名称，类似于ERC-20的名称
### symbol
符号，类似于ERC-20的符号
### uri
指向外部信息的链接，一般是一个JSON，而在JSON中有进一步更加具体的信息

## ERC-1155

ERC-1155 改进了 ERC-721：

### 单个合约能同时管理 FT 和 NFT
这主要通过tokenId来实现，该变量是一个uint256类型的变量，ERC-1155建议将这个256位的变量对半分，前128位作为base_token_id（可用于表示 NFT 的种类，如某个具体型号的手机），后128位作为index（可用于表示某种类下某个NFT的ID，如某个具体型号手机的序列号）。
### 支持批量转账
可以一次性转账多个种类的 FT 或者 NFT。
### 对uri所链接到的外部JSON文档的格式做了一些小改动

# NFT的应用场景

一切需要表示价值的场景都可以用到NFT。

## 实体经济

### 商品溯源
### 知识产权
### 证据存证
### 电子票据
### 电子证件

## 虚拟及金融资产

### 数字收藏品
比较有代表性的项目有：CryptoKitties、CryptoPunks、NBA Top Shot等。
### 游戏资产
比较有代表性的项目有：Gods Unchained、Axie Infinity、My Crypto Heroes等。
### 虚拟世界
比较有代表性的项目有：Decentraland、The Sandbox等。
### 加密艺术品
比较有代表性的项目有：Async Art、 SuperRare等。
### 金融
比较有代表性的项目有：Aavegotchi、Yinsurance等。
### 其他
比较有代表性的项目有：ENS等。

以太坊域名服务（Ethereum Name Service，简称 ENS）是一个基于以太坊区块链的分布式、开放和可扩展的命名系统，其将域名包装成了一个NFT。
