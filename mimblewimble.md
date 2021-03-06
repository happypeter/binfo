---
title: 写给 Bitcoiner 的 Mimblewimble 简介
---

Mimblewimble 是一个协议，跟 Bitcoin 相比(注意这里的 B 是大写，指的也是协议)， Mimblewimble 具有更好的隐私和可扩展性。

## 什么是 Mimblewimble？

我们首先介绍一下什么是 Mimblewimble？

聊一下这个名字的由来。 Mimblewimble 的提出者是一个化名为 Tom Elvis Jedusor（ 也就是《哈利波特》中的伏地魔）的神秘人士。Mimblewimble 是《哈利波特》中的一句咒语，可以让对方失去说话的能力，正如作者本人所说，Mimblewimble 之所以取这个名字就是因为它能阻止区块链去说出用户的信息。

Mimblewimble 的主要卖点就是隐私，这是通过融合了两项技术达成的。其中一项继承自 Adam Back 提出的机密交易（confidential transactions）。机密交易可以通过使用 blinding factors 来对交易金额进行加密。使用了机密交易之后，交易数额只有交易双方知道，但是网络上的其他人依然可以见证交易防止双花。Mimblewimble 的交易跟机密交易类似，不同的是发送方会选出很多 blinding factors，接收方会从中选出一部分，通过手里的这部分 blinding factors 来证明自己有权利使用接收到的币。另外一项是混币技术，说白点就是把比特币发送地址和接收地址的关系打断的一种技术，达到无法追踪的效果。

同时，Mimblewimble 还实现了非常好的可扩展性。隐私技术通常会让加密货币的性能下降，因为会涉及到大量的加密解密运算。而 Mimblewimble 却可以增加区块链的可扩展性，因为采用了 Mimblewimble 技术之后，很多过往的交易是可以删除的。

这样，我们就清楚了 Mimblewimble 名字的由来以及它的两个主要优势：隐私和可扩展性。

## 和比特币的融合

比特币由于交易历史可追踪造成了相对低的隐私度，使得人们对于 Mimblewimble 有了非常高的热情，但是想要把 Mimblewimble 实现到比特币代码之中是比较困难的。

困难的原因是 Mimblewimble 和现有的比特币代码是不兼容的。Mimblewimble 中没有地址、余额以及脚本这些概念，这样带来的好处是更高的存储效率更强的隐私，当然同时也有劣势，因为没有脚本，整个系统的可编程度就会降低。

那么有没有一种方式能让 Mimblewimble 服务比特币呢？可以考虑把 Mimblewimble 协议实现成比特币的一个侧链。在侧链条件下，用户可以把比特币转移到 Mimblewimble 侧链之上，这样就可以更为隐私的形式来使用比特币了。

当然，跟比特币配合的形式除了侧链这种直接配合，还可以考虑开发基于 Mimblewimble 的竞争币。这样，把比特币兑换成竞争币再去交易，Peter 认为也是非常可行的。

## Mimblewimble 的实现

说到竞争币，我们就会聊到实现了 Mimblewimble 的两个现有区块链项目：Grin 和 Beam。

[Grin](grin) 项目是 Mimblewimble 的一个实现。我们首先要明确协议是一个东西，而协议的实现是另外一个东西，例如 Bitcoin 是一个协议，而 Bitcoin Core 是它的一个实现。Mimblewimble 也是一个协议，而 Grin 就是 Mimblewimble 的一个实现。Grin 项目使用了自己的区块链和自己的加密货币，项目创始人也是用的化名。Grin 项目采用 Rust 语言开发，代码可以在 GitHub 上找到 https://github.com/mimblewimble/grin。

另外一个更新的项目叫做 Beam，https://www.beam.mw/ ，Beam 项目是用 C++ 开发的。

## 总结

总结来说，Mimblewimble 融合了机密交易以及混币技术，实现了更强的可扩展性和隐私。当然，这个技术的实际可行性还有待于进一步的验证。

参考
- https://motherboard.vice.com/en_us/article/gv5wej/lord-voldemort-tom-elvis-jedusor-is-trying-to-save-bitcoin-mimblewimble
- https://shimo.im/docs/g4pgZGQTkk4uR754
- https://bitcoinmagazine.com/articles/battle-privacycoins-what-we-know-about-grin-and-beams-mimblewimble/
