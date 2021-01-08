---
title: 互联网奠基人传之《自由软件之父-- Richard Stallman 》
---

Richard Stallman 是自由软件基金会创办人，顶级编程大师，有史以来最著名的黑客（没有之一）。也是电影《黑客帝国》里面的预言家 Morpheus ，以及作为互联网基石的 Linux 操作系统的主要作者之一。

## 自由软件运动

现在我们很多人言必称开源，但是其实开源运动之前，还有自由软件运动，而 Richard Stallman 就是自由软件运动的发起人。

Richard 是比尔盖茨的哈佛校友。但是不同的是，比尔盖茨当时只是一个小黑客，而 Richard 是跟 SUN 之父 Bill Joy 和 Java 之父 Gosling 同一个级别的编程大师，圈内不少人认为他的编程水平要比 Linux 之父 Linus 高。但是由于 Linux 项目太重大，大家认为，Linus 是世界上最著名的程序员，而 Richard 是有史以来最著名的黑客。

自由软件和开源软件是有区别的。但是，二者的区别不是那么清晰，所以“开源软件”官方的说法其实是 FOSS ，也就是 Free and Open Source Software 。如果具体想查看”自由软件“和”开源软件“的差异，可以对比 GPL v1 和 GPL v3 。这两个协议都是 Richard 撰写的，Linux 项目就是基于 GPL v1 发布的，Linux 可以认为是开源软件之祖。但是 Richard 觉得 v1 不够激进，所以才有了 v3 。粗略来讲，自由软件把大众对软件源码的控制权发挥到了极致，于是对商业化不是特别友好，而开源软件是兼顾公司的商业模式的。

Richard 是非常激进的。他讨厌 Copyright ，因为 Copyright 限制了普通人拥有和改动软件源码的权力，所以他主张 Copyleft ，Copyleft 意味着任何人都享有对源码的使用权和修改权，同时如果你在以 Copyleft 授权的代码的基础上添加了新的功能，那么你开发的功能也必须是 Copyleft 的。显然 Copyleft 是有病毒性的。

## 编程大师

接下来，说说 Richard 的主要软件作品。

第一个是 GNU 操作系统。这个要从一个有意思的故事说起，Richard 年轻时用到一个软件，结果发现有 Bug 。他于是找厂商要代码，说要帮助厂商修改一下，结果厂商说代码是有商业版权保护的，不能给他代码。Richard 觉得这个事情很不合理，能不能自己实现一套完全自由的操作系统呢？单枪匹马，说干就干， GNU 项目就诞生了。GNU 系统最终没有独立成名，但是 Linux 系统上绝大部分的软件都是来自 GNU 系统的，对，你没有听错，是绝大多数。

第二个是 Gcc 编译器。GNU 系统是由很多个软件组成的，其中一些的第一作者不是 Richard 。但是，Gcc ，也就是 GNU 的 C 编译器是出自 Richard 之手。没有 Gcc ，那么 Linus 后来就没有办法去编译 Linux 代码了。

第三个是 Emacs 编辑器。熟悉编辑器之战的人自然之道这款编辑器的江湖地位，不多说。

Richard 号称世界上写代码最多的人之一，所以作品很多，不一一列举了。

## 黑客帝国中的预言家

Richard 的江湖地位可以用电影黑客帝国的角色来做个比喻。

![](https://happypeter.github.io/images/2019072201.jpg)

Richard 发起自由软件运动，是时代的预言家。对应黑客帝国中的角色是预言家 Morpheus 。Morpheus 自己战斗力也很强，对应 Richard 也为 Linux 最终的腾飞奠定了坚实的基础。

自由软件对抗的是微软发起的商业软件运动。黑客帝国中那个大反派能够无限的复制自己，对应的现实人物就是比尔盖茨。乔布斯说过的：

> 在 Bill 之前，大家根本不知道软件还能独立成为一个行业

盖茨的主张就是卖 Copy ，对应电影中的人物有非常强的 copy 自己的能力。

革命的真正成功，关键人物是电影的主角 Neo 。GNU 系统发展了十年，但是系统的内核总是不太稳定，而 Linux 的出现弥补了这个缺憾。所以 Linus 就是 Neo 。

上面的对应关系，我是在网上看到的，不太清楚是不是黑客帝国编剧的本意，但是的确是很有说服力的，就连 Eric Steven Raymond ，也就是”开源“这个概念的主要提出者和阐释者，都在剧中有对应的角色。

## 总结

坦率的说，自由软件基金会和 Richard 本人的思想因为过于激进，多年来在美国主流社会中并不是很受欢迎。Linus 也说 Richard 对事物的认识过于非黑即白，Eric Steven Raymond 说：

> 并不是他的基本方向有什么问题，问题是他的那些言论说服不了任何人

尽管这样，美国也给了 Richard 麦克阿瑟天才奖，和科学院院士的地位。Peter 个人觉得，在未来，Richard 的主张有可能看起来就不那么激进了，在现在，世界能容得下他这样的人，也是让人感觉很幸福的事情。

最后用 Richard 的一句话来结束本文，这句话在大公司通过 App 垄断各个行业的今天，看起来格外有深意：

> If the users don't control the program, the program controls the users. With proprietary software, there is always some entity, the "owner" of the program, that controls the program and through it, exercises power over its users. A nonfree program is a yoke, an instrument of unjust power.

> 如果用户不能控制程序，程序就会控制用户。通过专有软件的形式，程序的所有者总是能够获得过多的权力，不自由的软件是不公正的权力诞生的温床。

参考：

- https://en.wikipedia.org/wiki/Richard_Stallman
