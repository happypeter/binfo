---
title: 比特币的 Nonce 是什么？
---

Nonce 这个单词在密码学语境下指的是一个只使用一次的数字。比特币的 nonce 是用在 POW 共识算法之中的一个数字。

## Header 中的 Nonce

比特币的每一个区块都有一个 header，header 中存储了多项关于区块的关键信息，其中就包含 nonce 。

Header 中包含的信息主要是下面几项：

- Version 。区块的版本号。
- 之前一个区块的 header 哈希。
- [Merkle](merkle) 根哈希。这个哈希是由区块中包含的所有交易的哈希值运算得出的，如果有人篡改了任何交易，这个哈希值就会变。header 中保留了这个值意味着只要 header 安全了，整个区块就安全了，这解释了为何计算 nouce 的时候，只需要计算 header 的哈希，而忽略区块主体数据。
- 时间。矿工开始运算 header 哈希的那个时间点。
- nBits 。压缩格式的 target 值。这一项是跟 nonce 紧密相关的，后面我们还会详细介绍。
- Nonce 。下面详细介绍。

所以，简单来说 nonce 就是每个区块 header 之中都会保存的一个数。


## Nonce 的计算步骤

计算 nonce 值的过程就是对区块 header 不断的运算哈希，直至找到能使区块哈希小于 target 的 nonce。

Target 就是一个 256-bit 的数。因为计算 header 哈希使用的[哈希算法](hash)是 Sha256 ，运算得到的哈希值是 256-bit 的一个数，所以恰好可以用来和 target 对比。所有比特币客户端在计算 nonce 的时候都使用相同的 target ，并且这个 target 值会被记录到 header 中，保存到了 nbits 这一项。nBits 是一个 32-bit 的数，所以保存的是 target 的压缩形式，具体换算关系可以参考[这篇文档](https://bitcoin.org/en/developer-reference#target-nbits)。Target 要小于这个数  0x00000000FFFF0000000000000000000000000000000000000000000000000000 。

每次计算 header 哈希就让 nonce 值加1。具体 nonce 的运算过程就是不断的修改 nonce 值，然后对这个 header 重新运算哈希的过程。每得到一个哈希值就去跟 target 对比，如果哈希小于或者等于 target ，那么运算过程就结束了，当前 nonce 值会被最终记录到 header 中。否则，就把 nonce 值加1，再次计算 header 哈希。显然，各个比特币客户端开始了一场寻找 nonce 的比赛，谁的硬件速度快，就有更大的概率率先找到 nonce 值，也就是宏观意义上抢到的记账权，当然，哈希的运算过程非常随机，所以这场比赛也跟抓彩票一样有很强的运气成分。

以上就是 nonce 的生成步骤了。


## Target 每两周调整一次

通过调整 target 值，可以来调整挖矿难度，挖矿难度每两周会调整一次。

Target 的值越小，挖矿难度就越大。POW 算法下的挖矿难度就体现在找到 nonce 值的难度，挖矿难度越大找到 nonce 值所需要的时间就越。寻找 nonce 意味着找到一个满足特定范围的区块哈希，这个范围越大找到满足条件的 nonce 就越容易，反之则越难。而这个范围就是大于零小于 target ，所以 target 越小，找到合适的 nonce 就越难。

挖矿难度每两周会调整一次。首先说，为什么要调整呢？由于寻找 nonce 的过程带有一定的随机性，每次找到 nonce 的时间都不一定是网络所期待的十分钟，所以如果时间大于十分钟，说明挖矿难度有可能设置的太高了，那么下一次我们就需要把挖矿难度降低，从而尽量保持平均找到 nonce 的时间是十分钟。而实际中，并不是每次出块后都会调整挖矿难度，比特币网络规定挖矿难度每2016个区块调整一次，2016个十分钟恰好是两周，所以每次难度调整的时间间隔是大约两周。

总之，伴随 target 的调整，挖矿难度也随着调整，可以保证平均的每次找到 nonce 的时间尽量趋近十分钟。

## 总结

理解 nonce 的运算过程是理解 POW 共识算法的核心，本节的内容就是这些了，需要记住的是以下几点：第一，nonce 是每个区块 header 中保存的一个数。第二，一旦找到合适的 nonce 让 header 的哈希小于 target 就意味着成功得到了最终的 nonce 。第三，为了保证平均起来每次找到 nonce 的时间趋近十分钟，target 会每两周调整一次。


参考：

- https://bitcoin.stackexchange.com/questions/71578/understanding-bits-and-difficulty-in-a-block-header
- https://www.mycryptopedia.com/bitcoin-nonce-explained/
- https://en.bitcoin.it/wiki/Block_hashing_algorithm
