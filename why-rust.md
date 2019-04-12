Rust 是一种2015年发布的新的编程语言，可以作为 C/C++ 或者一些更上层语言的替代品。你可能首先要问的一个问题是

> 为啥又要发明一种语言呢？

本文中我们来一起看看 Rust 到底强在哪里？

## 快

如果你目前使用的语言是类似 Ruby、Python 这样的较高层级语言，那可以试试 Rust ，因为 Rust 写出来的程序真的性能非常棒。

Rust 是一种编译型语言，类似 C ，可以对硬件进行直接的操作，所以执行起来会非常省资源并且非常快。Rust 非常适合写一些系统软件，换句话说就是写一些底层软件。所以在区块链圈子中，Rust 非常的流行，诸如 Grin 和 Nervos 这样的项目都在使用 Rust 。

Rust 遵从“零成本抽象”。Rust 提供了一些抽象，不然就不能提供出那些更高层级的语言才有的好用的语言特性。但是 Rust 的设计是非常巧妙的，会保证这些抽象是零成本的，也就是所有的抽象都会在编译过程中被处理，真正执行的时候是不依赖 Garbage Collector 或者其他的运行时的，也就避免了消耗资源。

Rust 跟其他的语言也能非常无缝的融合。Rust 可以通过 C ABI 的形式来跟其他语言实现零成本的对接。Rust 中可以使用 C 库，C 代码中也能直接使用 Rust 库。

下面来观察一个[例子](http://intorust.com/tutorial/why-rust/)，体会一下 Rust 的做事风格。Ruby 语言有一个方法叫做 blank ，用来做字符串是否为空的检查。Ruby 的实现是这样的。

```ruby
class ::String
  def blank?
    /\A[[:space:]]*\z/ == self
  end
end
```

代码是非常简单的，但是性能可不怎么样，每秒迭代次数为 964K 。

于是有[高手](https://github.com/SamSaffron/fast_blank
)使用 C 语言开发了一个高性能的版本

```c
#include <stdio.h>
#include <ruby.h>
#include <ruby/encoding.h>
#include <ruby/re.h>
#include <ruby/version.h>

#define STR_ENC_GET(str) rb_enc_from_index(ENCODING_GET(str))

#ifndef RUBY_API_VERSION_CODE
# define ruby_version_before_2_2() 1
#else
# define ruby_version_before_2_2() (RUBY_API_VERSION_CODE < 20200)
#endif

static VALUE
rb_str_blank_as(VALUE str)
{
  rb_encoding *enc;
  char *s, *e;

  enc = STR_ENC_GET(str);
  s = RSTRING_PTR(str);
  if (!s || RSTRING_LEN(str) == 0) return Qtrue;

  e = RSTRING_END(str);
  while (s < e) {
    int n;
    unsigned int cc = rb_enc_codepoint_len(s, e, &n, enc);

    switch (cc) {
      case 9:
      case 0xa:
      case 0xb:
      case 0xc:
      case 0xd:
      case 0x20:
      case 0x85:
      case 0xa0:
      case 0x1680:
      case 0x2000:
      case 0x2001:
      case 0x2002:
      case 0x2003:
      case 0x2004:
      case 0x2005:
      case 0x2006:
      case 0x2007:
      case 0x2008:
      case 0x2009:
      case 0x200a:
      case 0x2028:
      case 0x2029:
      case 0x202f:
      case 0x205f:
      case 0x3000:
#if ruby_version_before_2_2()
      case 0x180e:
#endif
          /* found */
          break;
      default:
          return Qfalse;
    }
    s += n;
  }
  return Qtrue;
}

static VALUE
rb_str_blank(VALUE str)
{
  rb_encoding *enc;
  char *s, *e;

  enc = STR_ENC_GET(str);
  s = RSTRING_PTR(str);
  if (!s || RSTRING_LEN(str) == 0) return Qtrue;

  e = RSTRING_END(str);
  while (s < e) {
    int n;
    unsigned int cc = rb_enc_codepoint_len(s, e, &n, enc);

    if (!rb_isspace(cc) && cc != 0) return Qfalse;
    s += n;
  }
  return Qtrue;
}


void Init_fast_blank( void )
{
  rb_define_method(rb_cString, "blank?", rb_str_blank, 0);
  rb_define_method(rb_cString, "blank_as?", rb_str_blank_as, 0);
}
```

性能提升了十倍还多，每秒迭代次数 10.5M ，但是写代码的时候要操多少心，看看上面的代码就知道了。

下面看看 Rust 的版本

```rust
exten "C" fn fast_blank(buf: Buf) -> bool {
  buf.as_slice().chars().all(|c| c.is_whitespace())
}
```

代码简单，执行效率比 C 的甚至还略快一点，每秒 11M 次迭代。

总之，Rust 非常的快，因为它的抽象都是零成本的，本质上是跟 C 一样的相对低层级的语言。

## 安全

如果你平常使用的是 C/C++ 这些相对低层级的语言，那么对硬件的控制能力就已经很充分了，但是 Rust 依然可能对你很有吸引力，因为 Rust 提供默认的安全保证，让可以让开发变得容易，让你成为一个效率更高的开发者。

C/C++ 提供了极高的灵活性，但是同时也让开发者面对各种的风险。C 语言可以实现非常高的性能，但是由于没有抽象层的保护，开发者很容易就会写出 Bug 。C++ 也类似，对开发者容忍度很低，一个很小的疏忽，就可能导致程序崩溃，其实崩溃还是幸运的，有时候会出现很低难以复现的诡异情况。Peter 自己第一份工作就是全职 C++ 开发者，感觉既要实现业务逻辑，还要同时讨好硬件，双份劳动，一份产出。后来切换到 Ruby 和 Python 这些高层级语言后，感觉就只需要关系业务逻辑即可了。

但是 Rust 真的很不一样，Rust 提供了很强的安全保证。使用 Rust 写的代码，运行的时候不会出现各种硬件安全问题，例如段错误，运行时崩溃，野指针，越界资源调用，或者 data race 。那么这是如何做到的呢？Rust 通过一定的语言层面的规定和强大的编译器支持来避免上面的情况。如果你是新手程序员，犯了上面的这些错误，编译的时候，编译器会直接告诉你存在的问题，而不会在程序运行的时候出现各种诡异的没有报错的状况。

Rust 有句口号是：Hack without fear 。只要程序编译是通过的，我们就不用再为程序的各种安全问题担心了。

## 人体工学

很多人喜欢 Ruby 语言，因为它

> 为程序员的快乐而优化

Rust 社区经常会提到的一个词就是“人体工学”，跟 Ruby 追求的目标是一致的，也就是让开发者非常的舒服。

Rust 是支持多种开发范式的，例如，generic, imperative, structured 等。同时借鉴 Haskell 等函数式语言，Rust 也对函数式编程有很好的支持。Rust 里面的变量默认就是 immutable 的，也就是拥有“不变性”的。这样的功能可不是 C/C++ 可以提供的，支持多范式，Peter 不确定是不是属于人体工学，但是不支持函数式编程的语言，用起来怎么可能 Happy 呢。

Rust 的工具生态也非常的好。Rust 有自己的包管理系统，跟 npm 类似，可以很方便的下载到需要的包，并进行依赖管理。编译系统也很完善，不需要手动去写 Makefile 了。

Rust 所有的贴心都来自于真正活跃的社区。Rust 是由 Mozilla 发起的项目，但是 80% 的对 Rust 的贡献是来自 Mozilla 之外的，可见 Rust 是一个真正属于社区的语言，对于很多人来说，使用的语言不被单一公司把持是至关重要的。

Rust 不仅仅关注执行效率，也关爱开发者，注意提高开发效率以及开发者幸福度。

## 总结

最后总结一下吧。Rust 在一个较低的层级上实现了各种高层级语言才有的方便特性。它和较低层级语言，例如 C/C++ 一样，高性能，同时又跟那些带有更多运行负担的较高层级语言，例如 Ruby/Python 或者 Haskell 一样，拥有自带的安全性和易用性。这就是为何很多人分别从更高或者更低层级的语言，切换到 Rust 的原因。
