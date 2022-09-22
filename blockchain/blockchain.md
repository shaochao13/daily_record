# Bitcoin

它是以密码学算法为基础，能够让人们以去中心化的方式，发生非许可的金融行为。

# Eth
`Vitalik Buterin` 2015年发布了`以太坊`。

在`以太坊`上，除了可以做去中心化的交易外，还可以签署去中心化的合同，构建去中心化的组织，以及在不需要中心化中介的情况下，以去中心化的方式进行协作。

# 智能合约

使用`比特币中的技术`，再加上`去中心化的合同`，即“智能合约”。

`Smart Contracts` are a set of instructions executed in a decentralized way without the need for a centralized or third party intermediary.

`智能合约`是通过`去中心化`的方式来执行一系列的指令，在这些指令执行中，并不需要中心化或者第三方的中介。

`智能合约`是部署在`去中心化区块链`上的`一个合约`或者`一组指令`,当这个合约或者这组指令被部署以后，它就`不能被改变`了(Cannot be altered/immutable)，它会`自动执行`(Automatically executes)，`每个人都可以看到合约中的条款`(Everyone sees the terms of the agreement)。


`智能合约`: `不可更改 Immutable`、`去中心化 Decentralized`、`透明的 Transparent`。

智能合约做什么(The purpose of Smart Contracts)？ `智能合约`创建了`信任最小化协议`(*Trust Minimized Agreements*)， 简单来讲就是创建`不可违背的承诺`(*Unbreakable Promises*)。

`区块链`的`目的`很简单：**就是来保证承诺不被违背**。

`以太坊`和`比特币`最大的`不同点`就是`智能合约`。

技术上讲，比特币有智能合约，但是比特币不是图灵完备的，也就是比特币不能执行一个编程语言的所有的指令。

比特币开发者想的是把比特币作为价值存储，而以太坊开发者除了把以太坊作为价值存储以外，还把它当成一个运行去中心化合约的平台。

`预言机`是任何可以向区块链输入数据或者进入链下计算的设备。 (`Blockchain Oracle`: Any device that interacts with the off-chain world to provide external data or computation to smart contracts.)

A Decentralized Oracle Network 一个去中心化的预言机网络。

将链上去中心化逻辑和链下去中心化数据和计算相结合，这个东西就叫做`混合型智能合约`(*Hybrid Smart Contracts*)。

`Dapp` = `Decentralized Application` 

`Web3`是一种观点，它指的是以`区域链`和`智能合约`为基础的下一代的网络。 在Web3中，用户拥有他们所使用的协议，即`拥有者经济`。

`DeFi` = `Decentralized Finance` 去中心化金融   
`DAO` = 去中心化自治组织    
`NFT` = 非同质化代币，它在某种程度上是一种电子艺术品。


# `Gas`

`Gas`: A unit of computational measurement.`gas`是一个计算量的单位   

The more complex your transaction is the more gas you have to pay. 要使用更多的计算资源，就需要支付更多的`gas`。

Any transaction on the blockchain comes with paying gas. 任何区块链上的交易，都需要支付交易手续费。

在区块链中，区块能存储交易的空间有限。

The most important thing, is that sending transactions gets more expensive the more people use the chain.

`Block Confirmations` 确认区块。

`确认区块数量`指：在交易被确认之后，有多少个区块被挖出。(Number of blocks mined since).如果看到确认区块是2，就表示在最长的链中，我们交易后面有2个区块。

`Gas fees` are paid by whoever makes the transaction. `gas fee`是由发起交易的人支付的。

# `SHA256` 哈希算法

`Hash`: A unique fixed length string, meant to identify a piece of data. They are created by placing saied data into a "hash function". `哈希`是一个独一无二的固定长度的字符串，用来代表一段数据，它是通过将一个数据传入“`哈希函数`”来生成的。

`Hash Algorithm`: A function that computes data into a unique hash.

`以太坊`用的是 `Keccak-256` 哈希算法。 

# 区块的组成

在`区块`中，把数据分成了：`块高`Block、`Nonce`和`Data` 三部分, 并将这三部分一起使用哈希算法来算出来一个哈希值。  

`Nonce`: A "number" used once" to find the "solution" to the blockchain problem. It's also used to define the transaction number for an account/address.

在区块链中，除了前面三个部分之外，还会多一个`prev`,它用来指向前一个“区块”的Hash。 将这四部分使用哈希算法算出来一个哈希值，这个哈希值就是当前这个“区块”的Hash。

`区块链中的区块由块高(Block)，Nonce，交易(Tx)和前一个区块哈希值(Prev)组成。`

Blockchain: A list of transactions mined together.

用`Tx`替代`Data`部分，`Tx`部分代表着这个区块中发生的所有交易。

`看一个区块是否有效最简单的方式：看它的Hash值，是以4个“0”开头的`。


`Genesis Block`: The first block in a blockchain。`创世区块`，是区块链中的第一个区块。创世区块的`prev`会指向一个并不存在的区块。

`Mining`: The process of finding the "solution" to the blockchain "problem". `挖矿`是找到区块链“难题”的“答案”的过程。 In our example, the "problem" was to find a hash that starts with `four zeros`. 在我们的例子中， 这个“难题”是找到一个以`4个0`开始的哈希值。  Nodes get paid for mining blocks. 节点通过挖矿来获得收入。

Decentralized: Having no single point of authority.

`Gas prices` are how much it costs to perform executions on-chain.

# Signing Transactions 签名交易

`Private Key`: Only known to the key holder, it's used to "sign" transactions.

`Public Key`: Is derived from your `Private Key`. Anyone can "see" it, and use it to verify that a transaction came from you. Anyone can then verify this new transaction hash with your `Public Key`.

ECDSA算法(Elliptic Curve Digital Signature Algorithm)椭圆曲线数字签名算法, 比特币和以太坊使用这个算法来生成Private Key。 它是`DSA`（电子签名算法）的一种，它可以根据`Private Key` 创建出`Public Key`。

用`Private Key` 来对`信息签名`，`Public Key`让别人来`验证签名`是你的。

`以太坊的地址`它是从`Public Key`衍生出来的，为`Public Key`最后的20个字节。但并不是所有的区块链的地址都是这样获取的。

# 区块链 Blockchain

每一个节点都保存着链上发生的所有交易记录。
Blockchain nodes keep lists of the transactions that occur.

## Consensus

`Consensus`(共识)、`工作量证明`、`权益证明`。`工作量证明`和`权益证明`都属于共识。

`Consensus` is the mechanism used to agree on the state of a blockchain. `共识`是一个机制，通过这个机制，区块链可以在状态和数值上达成一致。

`Consensus` is how blockchains decide what the state of the chain is. 共识是区块链确定当前状态的机制。

区块链或者去中心化系统的共识协议，可以非常粗略的分为两部分：`Chain Selection`链的选择算法 和 `Sybil Resistance`抗女巫攻击机制。

`Chain Selection` 用来确定哪个区块链是正确的链。

在`比特币`和`以太坊1.0`中，它们用的共识叫`Nakamoto Consensus 中本聪共识`， `Nakamoto Consensus`包括了`工作量证明`和`最长链规则`。

### Sybil Resistance

`Sybil Resistance` 是一种区块链的能力，来防止用户使用大量的假身份，在整个系统，来获取超出应有比例的权益和影响力。通俗地说，它防止某些人创建假的节点，然后获取得越来越多的奖励。

> 两种抗女巫机制`Sybil Resistance` ： `Pow`(Proof Of Work)工作量证明 和 `Pos`(Proof of stake)权益证明。

#### PoW

`Proof of Work` uses a lot of energy.

> 在`工作量证明`网络，节点会彼此竞争来解决区块链“难题”。依据区块链的不同，这个“难题”会有些不同。所有的节点会尽可能多的尝试，以便能第一个找到“难题”的答案。

第一个找到答案的节点会获得`收入`，收入分两部分：`交易手续费 Transaction Fees` 和 `区块奖励`。

> `交易手续费 Transaction Fees`就是为了写入交易而支付的手续费。     
> `区块奖励`是由区块链协议自身发给节点的。      
> `减半`指的是区块奖励减少一半。 比特币是大概每4年减半一次。        

在比特币中，会设置一个时间点，过了这个时间点就会取消区块奖励，到时矿工或者节点只能获得交易手续费。


`出块时间`是每个区块被发布之间的时间，它和这些算法的难度相关。

挖矿或者是工作量证明算法，是一种抗女巫攻击机制。以太坊2.0之后就不是工作量证明了，而使用权益证明。

两个可能存在的攻击：
1. `Sybil Attack` 女巫攻击，在攻击中，用户会创建很多匿名账户，来影响区块链。
2. `51% Attack` 作为共识协议的一部分，最长的链会被选择为正确的链，同时要满足和网络的51%相一致。这意味着，如果你有最长的链和51%的网络，那就可以分叉区块链，让整个网络使用你的链

#### PoS

`Proof of stake` nodes put up collateral as a sybil resistance mechanism. `权益证明`需要放置一些`抵押物`以保证不作恶。

在以太坊2.0中，节点需要质押以太币以保证自己会诚实运行。如果它们没有诚实运行，它们会被踢出，或者质押会被扣掉。

在权益证明的网络中， 矿工被称作`验证者Validators`。他们不再挖矿了，他们只验证其他节点。 在权益证明的网络中，节点会被直接选举出来，然后提出一个区块，别的节点会验证这个被提出的区块是否有效。

权益证明网络的`优点`：
- 它有很好的抗女巫攻击机制，可以很好决定哪个节点来提议下个区块。
- `绿色环保`。 获得新的区块所需的计算量大大降低 Proof of stake uses much less energy。只需要一个节点来做计算，其他节点来进行验证。

权益证明网络的`缺点`：
- 它被认为有一些`不够去中心化`。
- 因为有质押的花费，这是参与权益证明的花费

`Randomness`随机性。 每个区块链选择节点的方式都不同，以太坊2.0使用了`RANDAO`

在权益证明的网络中，也有交易手续费，这个费用是支付给验证者的。


## `Scalability`可扩展性

可扩展性问题，是因为区块空间不足导致的写入的交易有限。Only so many transactions can fit into a block. 这会导致很高的`gas price`.

`layer1`的可扩展性问题的解决方案：`Sharding` 和 `Rollup`.
`Sharding` and `Rollup` are scalability solution.

### `Sharding` 分片

`Sharding` 分片， 就是可扩展性问题的一种解决方案。区块链的分片指的是多个区块链的区块链有一个主链会协调一些不同的链，将他们连接在一起。这意味着，可以在多个链上发送交易，很有效率地提高了区块链的空间。

> `Sharding`分片可以极大地增加在`layer 1`上发送的交易数量。

`Layer 1`: Base layer blockchain implementation. `layer 1`是区块链实现的`基础层`。 `比特币`、`以太坊`和`avalanche`都是`layer 1`,这些是区块链基础层的解决方案。

`Layer 2`: Any application built on top of a `layer 1`. `layer 2` 是加在 `layer 1 `和区块链上的任何应用。比如：`Chainlink`, `Arbitrum`, `Optimism`等。

`Eth2.0`开始使用`PoS 权益证明`和`Sharding 分片`。

### `Rollup` 

`Rollup`: 把layer2上的它们自己的交易集中起来，然后写入以太坊这样的layer1中。它有点像一个分片的链，它继承了以太坊这样的基础链也就是layer1的安全性。它们都把交易发给layer1。作为一条链，人们在它上面交易就相当于在以太坊上发交易。

`layer 2 `和`侧链`不同，因为侧链的安全性来自于自身协议，而`Rollup`的安全性来自于基础层。

`Arbitrum`和`Optimism`就是`Rollup`,它们和以太坊是一样安全的。


谁得到了交易手续费？是矿工或者叫验证者。在工作量证明的网络中，叫矿工，在权益证明的网络中，叫验证者。