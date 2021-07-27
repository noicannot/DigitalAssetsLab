- [以太坊基础](#以太坊基础)
  - [以太网货币单位](#以太网货币单位)
  - [选择一个以太坊钱包](#选择一个以太坊钱包)
  - [切换网络](#切换网络)
    - [Main Ethereum Network](#main-ethereum-network)
    - [Ropsten Test Network](#ropsten-test-network)
    - [Kovan Test Network](#kovan-test-network)
    - [Rinkeby Test Network](#rinkeby-test-network)
    - [Localhost 8545](#localhost-8545)
    - [Custom RPC](#custom-rpc)
  - [使用MetaMask发送ether](#使用metamask发送ether)
  - [世界计算机简介](#世界计算机简介)
  - [外部所有账户（EOAs）和合约](#外部所有账户eoas和合约)
  - [一个简单的合约：一个test ether faucet](#一个简单的合约一个test-ether-faucet)
  - [编译faucet合约](#编译faucet合约)
  - [在区块链上创建合约](#在区块链上创建合约)
  - [与合约交互](#与合约交互)
    - [在区块浏览器中查看合约地址](#在区块浏览器中查看合约地址)
    - [为合约提供资金](#为合约提供资金)
    - [从我们的合约中提取](#从我们的合约中提取)

# 以太坊基础

## 以太网货币单位

以太坊的货币单位称为 以太 ether，也被称为ETH或符号 Ξ （来自看起来像程式化的大写字母E的希腊字母“Xi”）或（不太常见的）♦，例如，1个以太，或1个ETH，或 Ξ1，或 ♦1

一个 ether 是 $1× 10^{18}$ 或1,000,000,000,000,000,000 个 wei。

以太坊是制度，以太是货币。

| Value (in wei)                    | Exponent | Common Name | SI Name               |
| --------------------------------- | -------- | ----------- | --------------------- |
| 1                                 | $1$        | wei         | wei                   |
| 1,000                             | $10^3$      | babbage     | kilowei or femtoether |
| 1,000,000                         | $10^6$      | lovelace    | megawei or picoether  |
| 1,000,000,000                     | $10^9$      | shannon     | gigawei or nanoether  |
| 1,000,000,000,000                 | $10^{12}$     | szabo       | microether or micro   |
| 1,000,000,000,000,000             | $10^{15}$     | finney      | milliether or milli   |
| ***1,000,000,000,000,000,000***       | $\pmb10^{\pmb18}$   | ***ether***     | ***ether***               |
| 1,000,000,000,000,000,000,000     | $10^{21}$     | grand       | kiloether             |
| 1,000,000,000,000,000,000,000,000 | $10^{24}$     |             | megaether             |

## 选择一个以太坊钱包

别担心！如果你选择一个钱包而不喜欢它的工作方式，那么你可以很容易地更换钱包。你只需进行一项交易，即将资金从旧钱包发送到新钱包，或者通过导出和导入私钥来移动密钥。

## 切换网络

默认情况下，MetaMask将尝试连接到“主网络”。其他选择是公共测试网，你选择的任何以太坊节点或在你自己的计算机上运行私有区块链的节点（本地主机）：

### Main Ethereum Network

主要的，公开的以太坊区块链。真正的ETH，真正的价值，真正的后果。

### Ropsten Test Network

以太坊公开测试区块链和网络，使用工作证明共识（挖矿）。在这个网络上的ETH没有价值。Ropsten的问题在于攻击者铸造了数以万计的区块，产生巨大的重组并将燃气极限推到9B。当时需要一个新的公共测试网，但之后（2017年3月25日）Ropsten也复活了！

### Kovan Test Network

以太坊公开测试区块链和网络，使用“Aura”协议进行权威证明（Proof-of-Authority）共识（联合签名）。在这个网络上的ETH没有价值。该测试网络仅由“Parity”支持。其他以太坊客户使用稍后提出的"Clique"协议作为权威证明。

### Rinkeby Test Network

以太坊公开测试区块链和网络，使用“Clique”协议进行权威证明共识（联合签名）。在这个网络上的ETH没有价值。

### Localhost 8545

连接到与浏览器在同一台计算机上运行的节点。该节点可以是任何公共区块链（主要或测试网络）或私人测试网络的一部分。

### Custom RPC

允许你将MetaMask连接到任何具有geth兼容的远程过程调用（RPC）接口的节点。该节点可以是任何公共或私有区块链的一部分。

## 使用MetaMask发送ether

我们有1个ETH，我们想要发送1个ETH，为什么MetaMask说我们没有足够的资金？

答案是因为_gas_的成本。以太坊交易需要支付矿工收取的费用，以验证交易。以太坊的费用以_gas_虚拟货币收取。作为交易的一部分，你使用ether支付gas。

> 测试网络也需要费用。如果没有费用，测试网络的行为将与主网络不同，从而使其成为不适当的测试平台。费用还可以保护测试网络免受拒绝服务攻击和构造不良的合约（如无限循环），就像保护主网络一样。

当你发送交易时，MetaMask 计算出最近成功交易的平均天然气价格为3 gwei。发送基本交易的gas成本为21000个gas单位。因此，你花费的ETH的最大数量为3 * 21000 GWEI = 63000 GWEI = 0.000063 ETH。请注意，平均gas价格可能波动，因为它们主要由矿工决定。我们将在后面的章节中看到如何增加/减少gas限制，以确保你的交易在需要时优先处理。

这表明：1 ETH交易的成本是1.000063 ETH。MetaMask在显示总数时会将此近似到1 ETH，但你需要的实际金额为1.000063 ETH.

## 世界计算机简介

加密货币功能是服务于以太坊作为世界计算机的功能; 一个去中心化的智能合约平台。以太旨在用于支付运行的 smart contracts，这是在称为_Ethereum虚拟机（EVM）_的模拟计算机上运行的计算机程序。

EVM是一个全球性的单例，这意味着它的运作方式就好像它是一个全球性的单实例计算机，无处不在。以太坊网络上的每个节点运行EVM的本地副本以验证合约执行，而以太坊区块链记录此世界计算机在处理交易和智能合约时变化的状态。

## 外部所有账户（EOAs）和合约

我们在MetaMask钱包中创建的账户类型称为 Externally Owned Account（EOA） 。外部所有账户是那些拥有私人密钥的账户，它控制对资金或合约的访问。现在，你可能猜测还有另一种帐户，合约帐户。合约账户由以太坊区块链记录，由EVM执行的软件程序的逻辑所拥有（和控制）。

将来，所有以太坊钱包可能会作为以太坊合约运行，模糊了外部所有账户和合约账户之间的区别。但是永远保持的重要区别在于：人们通过EOA做出决定，而软件通过合约做出决定。

合约有一个地址，就像EOAs（钱包）一样。合约可以发送和接收ether，就像钱包一样。当交易目的地是合约地址时，它会导致该合约在EVM中_运行_，并将交易作为其输入。

## 一个简单的合约：一个test ether faucet

以太坊有许多不同的高级语言，所有这些语言都可用于编写合约并生成EVM字节码。

本书的合著者Gavin Wood创建了Solidity，已经成为以太坊及以太坊外最广泛使用的语言。

这是一个非常简单的合约。这也是一个有*缺陷*的合约，显示了一些不良做法和安全漏洞。

我们的真正的合约开始的地方：

    contract Faucet {

该行声明了一个合约对象，类似于JavaScript，Java或C++等其他面向对象语言中的 class 声明。合约的定义包含了大括号中的所有行 {}，它定义了 +范围 +，就像在其他许多编程语言中使用花括号一样。

接下来，我们声明faucet合约的第一个函数：

    function withdraw(uint withdraw_amount) public {

函数名为 withdraw，它接收一个无符号整数（uint）名为 withdraw_amount 的参数。它被声明为 public 函数，意味着它可以被其他合约调用。函数定义在花括号之间：

    require(withdraw_amount <= 100000000000000000);


withdraw+方法的第一部分设置了取款限制。它使用内置的Solidity函数 +require 来测试前提条件，即 withdraw_amount 小于或等于100000000000000000 wei，等于0.1 ether。如果使用 withdraw_amount 大于该数量调用 withdraw 函数，则此处的 require 函数将导致合约执行停止并失败，并显示_异常_。

它通过设定提款限额来控制合约的资金流出。

接下来是实际提款：

    msg.sender.transfer(withdraw_amount);

msg 对象是所有合约可以访问的输入之一。它代表触发执行此合约的交易。属性 sender 是交易的发件人地址。函数 transfer 是一个内置函数，它将ether从合约传递到调用它的地址。transfer 函数将一个金额作为唯一的参数。我们传递之前声明为 withdraw 方法的参数的 withdraw_amount 值。

紧接着的一行是结束大括号，表示 withdraw 函数定义的结束。

下面我们又声明了一个函数：

    function () public payable {}

此函数是所谓的_“fallback”_或_default_函数，如果合约的交易没有命名合约中任何已声明的功能或任何功能，或者不包含数据，则触发此函数。合约可以有一个这样的默认功能（没有名字），它通常是接收ether的那个。这就是为什么它被定义为 public 和 payable 函数，这意味着它可以接受合约中的ether。除了大括号中的空白定义 {} 所指示的以外，它不会执行任何操作。如果我们进行一次向这个合约地址发送ether的交易，就好像它是一个钱包一样，该函数将处理它。

在我们的默认函数下面是最后一个关闭花括号，它关闭了合约 faucet 的定义。

## 编译faucet合约

我们需要使用Solidity编译器将Solidity代码转换为EVM字节代码，以便它可以由EVM执行。为了简单起见，我们将使用一种更流行的IDE，称为Remix。

使用你的Chrome浏览器（使用我们之前安装的MetaMask钱包）导航到以下位置的Remix IDE：

https://remix.ethereum.org/


如果出现问题，最可能的问题是Remix IDE正在使用与0.4.19版本不同的Solidity编译器。在这种情况下，我们的编译指示将阻止Faucet.sol编译。要更改编译器版本，请转到“Settings”选项卡，将版本设置为0.4.19，并重试。

Solidity编译器现在已将我们的+ Faucet.sol +编译为EVM字节码。字节码如下所示：

    PUSH1 0x60 PUSH1 0x40 MSTORE CALLVALUE ISZERO PUSH2 0xF JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST PUSH1 0xE5 DUP1 PUSH2 0x1D PUSH1 0x0 CODECOPY PUSH1 0x0 RETURN STOP PUSH1 0x60 PUSH1 0x40 MSTORE PUSH1 0x4 CALLDATASIZE LT PUSH1 0x3F JUMPI PUSH1 0x0 CALLDATALOAD PUSH29 0x100000000000000000000000000000000000000000000000000000000 SWAP1 DIV PUSH4 0xFFFFFFFF AND DUP1 PUSH4 0x2E1A7D4D EQ PUSH1 0x41 JUMPI JUMPDEST STOP JUMPDEST CALLVALUE ISZERO PUSH1 0x4B JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST PUSH1 0x5F PUSH1 0x4 DUP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP2 SWAP1 POP POP PUSH1 0x61 JUMP JUMPDEST STOP JUMPDEST PUSH8 0x16345785D8A0000 DUP2 GT ISZERO ISZERO ISZERO PUSH1 0x77 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST CALLER PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH2 0x8FC DUP3 SWAP1 DUP2 ISZERO MUL SWAP1 PUSH1 0x40 MLOAD PUSH1 0x0 PUSH1 0x40 MLOAD DUP1 DUP4 SUB DUP2 DUP6 DUP9 DUP9 CALL SWAP4 POP POP POP POP ISZERO ISZERO PUSH1 0xB6 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP JUMP STOP LOG1 PUSH6 0x627A7A723058 KECCAK256 PUSH9 0x13D1EA839A4438EF75 GASLIMIT CALLVALUE LOG4 0x5f PUSH24 0x7541F409787592C988A079407FB28B4AD000290000000000

## 在区块链上创建合约

在区块链上注册合约涉及创建一个特殊交易，其目标是地址0x0000000000000000000000000000000000000000，也称为_zero address_。零地址是一个特殊的地址，告诉以太坊区块链你想注册一个合约。

Remix IDE将为你处理所有这些交易并将交易发送给MetaMask。

Remix IDE将构建特殊的“creation“交易，MetaMask会要求你批准它。从MetaMask中可以看到，合约创建交易没有ether，但它有258个字节（编译的合约），并且会消耗10个Gwei。

合约在Ropsten上开采需要大约15到30秒的时间。

合约有自己的地址。

## 与合约交互

以太坊合约是控制货币的程序，运行在名为EVM的虚拟机内。它们是由一个特殊的交易创建的，该交易提交它们的字节码以记录在区块链中。一旦他们在区块链上创建，他们就拥有一个以太坊地址，就像钱包一样。只要有人将交易发送到合约地址，它就会导致合约在EVM中运行，并将交易作为其输入。发送到合约地址的交易可能包含以太网或数据或两者都有。如果它们含有ether，则将其“存入”合约余额。如果它们包含数据，则数据可以在合约中指定一个命名函数并调用它，并将参数传递给该函数。

### 在区块浏览器中查看合约地址

在 ropsten.etherscan.io 区块浏览器中查看

### 为合约提供资金

现在，合约其历史上只有一笔交易：合约创建交易。

当你将交易发送到合约地址时，没有指定要调用哪个函数的数据，它将调用默认函数。由于我们将它声明为payable，因此它接受1 ether并存入合约账户余额中。你的交易导致合约在EVM中运行，更新其余额。


    function () public payable {}

### 从我们的合约中提取

提款的交易在“内部交易”里。由于0.1 ether传输源于合约代码，因此它是一个内部交易（也称为message）。