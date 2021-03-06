---
title: 伪随机数
---

计算机程序中使用的随机数通常都是用真随机数做种子去生成的伪随机数。那么什么叫真随机数，如何去生成伪随机数，真伪随机的安全性方面都什么可以量化度量的差异吗？

## 真随机数

先看看如何获得真随机数？

自然界中的有很多不确定的现象，例如一片沙漠中的各个沙粒的重量，或者大气中分子的热运动轨迹，通过对这些现象的测量，就可以获得真随机数。

优质的真随机源头就是那些人类还无法把握其规律的自然现象。

## 伪随机数

计算机程序中一般都是用伪随机。

计算机首先要获得真随机数来做伪随机数算法的种子。真随机数可以从从自然现象中获取，例如读取一段时间耳机收到的噪音，或者内存条上的分子热运动信息。

为何需要种子呢？计算机程序运行的结果是确定性的，输出的结果是可以预测的，而且是可以重复的，所以通过计算机程序是不能生产随机数的。但是有了种子，就可以去衍生出很多足够随机的随机数，也就是伪随机的数。

为何需要生成伪随机数呢？如果程序运行需要很长或者很多的随机数，而能够获得的真随机数的长度和数量又都有限，那么就会用程序去生成伪随机数。

来举一个简单的伪随机生成算法的例子。如果真随机数是121，那么可以把真随机数相乘然后取中间数的方式来获得伪随机数。121乘以121是14641，那么去掉开头和末尾，取中间数就获得了中间数464。这个464就是伪随机数，而121就是它的种子。如果要生成第二个伪随机数，就可以把464作为种子重复相同的操作。

总之，伪随机数是以真随机数为种子去按照算法生成的。

## 真随机和伪随机的区别

那么真随机数和伪随机数有没有什么区别呢？

按照真随机数的提取方法，不管取多少次，都可以看到各个输出是无规律的。但是伪随机数是计算出来的，如果原始种子比较短，很快伪随机数就出现周期性的重复了。当然，种子越长，周期也就会越长。两位数的种子，能够生产100个伪随机数，也就是说，周期是100，三位种子的周期是1000。

给定位数长度，真随机数安全性比较高。而伪随机的特点就是可以方便的获取多个，或者由较短的真随机能够获得一个程序所需要的较长的伪随机，但是伪随机是有一定规律的，同样位数的伪随机肯定没有真随机安全。不过，伪随机数的周期越长，就越安全。

## 总结

总结一下，真随机数来自自然现象，伪随机数是计算机把真随机数做种子通过算法生成的。

参考：

- https://www.khanacademy.org/computing/computer-science/cryptography/crypt/v/random-vs-pseudorandom-number-generators
