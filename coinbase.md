---
title: 什么是 Coinbase 交易？
---

比特币区块链上的每个区块之中都会包含一个或者多个交易（ transaction ），其中第一个交易就叫做 Coinbase 交易。

## 什么是 Coinbase 交易？

Coinbase 交易是矿工创建的，主要是为了奖励矿工为了进行 [POW 挖矿](pow-tech)而付出的努力。

奖励分为两部分。一部分是出块奖励，这部分是相对固定的，当前每个区块的出块奖励是12.5BTC，每四年减半一次。另外一部分是手续费，当前区块的每个交易中都会包含一定的对矿工的奖励，也就是交易手续费。创建 Coinbase 交易的时候，矿工会把所有交易中的手续费累加到一起，然后把这笔钱转账给自己。

Coinbase 交易的特点是没有“父交易”。普通交易中需要 input ，而 input 是来自父交易的 output ，所以普通交易是有父交易的。但是 Coinbase 交易是没有父交易的，因为币是直接由系统生成的。

## 什么是 coinbase ？

那么 coinbase 交易中的 coinbase 这个词是什么意思呢？

简单来说 coinbase 就是系统生成的币。“Coinbase 交易”也叫做 “Generation 交易”，也就是“生成交易”，这是因为其他的普通交易中，都是去转账已有的比特币，而这个交易是专门从无到有的去生成新的比特币的。精确一点说，coinbase 就是“生成交易”中的 [input](utxo) 。

这就是 coinbase 这个词的基本含义。

## Coinbase 交易中包含的数据

下面来仔细聊聊 coinbase 交易中包含的各项数据。

交易中包含一个 input 和一个 output 。这个 input 就是 coinbase 。output 指向矿工的地址，总金额等于 coinbase 加上区块中全部交易的手续费。

另外 coinbase 中还有一个最多100字节的数据。除了最开始的几个字节，这个数据中剩下的地方可以存储任意数据。矿工可以用来存储任何自己想要存储的数据。例如在创世区块，也就是 genesis block 中，中本聪保存了这样一句话：

>The Times 03/Jan/2009 Chancellor on brink of second bailout for banks

数据的最开始几个字节保存的是区块高度。所谓区块高度就是当前区块跟创世区块之间间隔的区块数量。创世区块就是比特币区块链上的第一个区块，区块高度是零，依次类推。

## 总结

关于什么是 coinbase 交易，咱们就介绍到这里了。重点信息有这么几项：首先，coinbase 交易是矿工自己构建的，用于把出块奖励和手续费奖励给自己。第二，coinbase 这个词本身可以理解为“系统最初生成的比特币”。第三，交易中包含一个 input 一个 output 和一段不大于100字节的数据。

最后要提醒一下，有一家美国的交易所也叫 Coinbase ，跟我们这里的概念同名，不要混淆。

参考：

- https://en.bitcoin.it/wiki/Coinbase
- https://www.mycryptopedia.com/coinbase-transaction-explained/
