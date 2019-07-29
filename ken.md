---
title: 互联网奠基人传之《 Unix 之父-- Ken Thompson 》 
---

1943年出生的 Ken Thompson 是 Unix 操作系统之父，由于 Unix 和互联网的紧密联系，所以 Peter 认为 Ken 也是互联网的奠基人之一。

![](https://img.haoqicat.com/2019072801.jpg)

## Unix 诞生

先简单介绍一下 Ken 的生活轨迹以及 Unix 是如何诞生的。

1965 Ken 在 UC Berkeley 获得了计算机硕士学位。1966年开始为贝尔实验室工作，并和好友 Dennis Ritchie 一起开始开发一个庞大而复杂的操作系统名叫 Multics 。Multics 最终因为过于复杂而失败，而 Ken 为了运行自己的游戏而在度假的时候开发的 Unix 操作系统却最终成为了操作系统之王。

早期的 Unix 主要是 Ken 一个人的作品。整个1970年代，Ken 和 Dannis 都在忙着开发 Unix 操作系统。为了开发 Unix ，Ken 自己还开发了 B 语言。B 语言启发了 Dennis Ritchie 的 C 语言，Unix 后来全部用 C 语言重写了一遍。这就是为何 Dennis 也被称为 Unix 之父的原因。

总之，Unix 的诞生是 Ken 的妙手偶得，Ken 也因此和 Dannis 一起获得了1983年图灵奖。

## Unix 和开源

Ken 不是 Richard Stallman ，也不是 Linus ，但是可以说，没有 Unix 也就没有开源软件。

Unix 本身是专有软件，但是其实 Unix 的源码是很容易拿到的。因为是在贝尔实验室员工的成果，所以 Unix 本身并不是开源软件。但是通过 Ken 和大家的努力，各个学校只需要花200美金就可以拿到 Unix 的源码。后来 Linus 写 Linux 的时候，其实也参考了很多已有的代码。

Unix 哲学是模块化哲学。Unix 的思想主张，每一个软件都只做一件事，并把这件事做好，同时定义好清晰的和其他软件通信的接口，以便不同的软件可以良好的配合。这种思想导致多人协作开发一个大系统变得非常容易，非常适合开团队组织松散开源团队来开发。

Ken 和 Dennis 说过

> 我们希望构建的不仅仅是一个优秀的计算平台，而是一个可以围绕它来形成一个编程社区的平台。

Linus 在作 The Origins of Linux ，也就是《 Linux 的起源》，演讲的时候，Ken 也在现场。Ken 和 Linus 讨论了社区化软件开发的哲学。Linus 当时给出了一段非常长的回答。Linus 说开源软件有自己的生命，会不断的进化。讨论过程中的思想，Peter 感觉不局限于软件开发，也体现出互联网的整个基础设施是如何慢慢自由生长的，非常值得推荐。

Linux 严格来说不算是 Unix 系统，因为虽然外在特征跟 Unix 几乎一模一样，但是系统内核的内部实现其实相差甚远，所以只是一个 Unix-like 系统。有意思的是，Ken 自己目前也使用 Linux 操作系统。目前安装量最大的 Unix 系统是苹果的 macOS 。

Unix 和开源是密不可分的，可以说没有 Unix 就没有开源社区。

## Unix 和互联网

同时，Unix 和互联网的联系，并不局限于 Unix 启发了 Linux 。

当年，Tim Berners-Lee 开发 Web 的时候，使用的就是 Unix 系统。第一个 Web 服务器是运行在乔布斯的 Nextstep 系统上的，而 Nextstep 系统就是现在的 macOS 系统的前身，就是 Unix 系统。于是，Unix 的很多特性都深深的刻入了互联网的基因之中。

另外 Ken 还参与了一些其他对互联网有重大影响的项目。1992年，Ken 参与制定了 UTF-8 编码标准，UTF-8 后来成了 Web 上编码的事实标准。另外，从2006年开始 Ken 在谷歌工作，发明了 Go 语言。Go 目前在互联网开发领域也是非常流行的。

也可以说，没有 Unix 就没有互联网。

## 总结

最后总结一下。 Ken 首先是现在计算机编程混沌初开时代的开山祖师。确定了之后几十年软件应该怎么搞，行业中有句话，

> 真正的程序员是用 Unix 的，真正的程序员是用 C 的。

Ken 不仅仅开发了各项互联网的基础技术，还为后来的整个开源运动打好了基础，所以 Ken 是当之无愧的互联网奠基人之一。

参考：

- https://en.wikipedia.org/wiki/Ken_Thompson#Early_life_and_education
- https://www.youtube.com/watch?v=tc4ROCJYbm0
- https://www.youtube.com/watch?v=WVTWCPoUt8w&t=56s
