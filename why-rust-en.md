---
title: Why Rust?
---

Rust is a new programming language released on May 15th 2015, providing an alternative to C/C++, but also higher-level languages. So the obvious question is 

> Why yet another programming language ?

Now we are going to give the answer by showing what's rust's true strengths are.

## It's Fast

If you are using high-level languages runing on top of a interperter, say Ruby, Python or Haskell, you should try rust if you want your app to be more performant.


Rust is a compiled language, like C, it controls hardware resource directly, that why Rust code runs very fast. It is Good for writing system software. A lot of blockchain projects are using Rust, because app writen in Rust can be really performat, due to Rust's ablity to fully control the hardware.

Rust offers zero-cost abstraction. Rust has a lot of the sweet high level language feathure over some abstraction as we will show you later. Bust Rust is carefully designed, so that all these abstractions are at no cost. That is compiler will take care of them, and no runtime or garbage collector is required to have these abstractions.

Rust plays well with other languages. Rust interfaces to other languaages throught the C ABI at zero cost. you can use C lib esaily in Rust Code, or use Rust lib in C code.

Now let's have a look at a example. Ruby has a method named `blank`, which is used to check if a string is blank or not. The ruby implementation of blank is like this.

```ruby
class ::String
  def blank?
    /\A[[:space:]]*\z/ == self
  end
end
```

It looks simple, but the performance is not so good, 964K iteration/sec.

So some [cool dude](https://github.com/SamSaffron/fast_blank) developed fast version blank with C.


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

It is ten times more performant, 10.5M iteration/sec. 

But finally let's look the implementation in Rust.

```rust
exten "C" fn fast_blank(buf: Buf) -> bool {
  buf.as_slice().chars().all(|c| c.is_whitespace())
}
```

Much simpler code, thanks to Rust's high level language features, and it's as perfomant,  11M iter/sec. 

So we can see Rust is really fast, because it's zero-cost abstaction.

## It's safe

To those who is using C/C++ and already have full control of the hardware, you still should try rust if you want to be a more efficent developer, cause Rust offers the safty guanranteses, that makes development so much easier.

C/C++ offers great power, but also lots of risks. C can implement extraordinary performance but with lower abstraction and results in human mistakes easily. Like C, C++ can be really unfogiving, small mistakes, carsh is only a lucky, you might be trapped in a very unclear situation. If you are using C/C++, You need to worry about the hardware machine, and at the same time, you need to worry about your logic of your app.

However, Rust gives us stong Safty guanranteses. No seg fault, no run time crash, no null pointer, no dangling pointers, no out-of-bound accesses. and data Race free. Rust achieve this buy certain language features and good compiler support for this. If ever you do some thing wrong, the compiler will tell you about it.

Hack without fear is Rust's slogan. You do not worry about your program once the compilation is complete.

## It's ergonomic

A lot of people love Ruby, cause it is

>Optimized for Programmer Happiness.

Rust does the same and is ergonomic.

Rust supports mutiple programming paradigms, like generic, imperative, structured. It is also inspired by Haskell,  you can do fp with rust. For example, you can explicitly define a variable to be utable with Rust. But by default, erveything is immutable. That sort of sweetness is not C/C++ can offer.

Rust has great tooling. Rust has a npm like system that you can get the ready-made code as packages. Cargo do the package managment for you. Rust also has great build system, no more hand made Makefiles.

Great community. More then 4/5 of contributions to Rust languange come from outside Mozilla. Compiler has more then 2000 contibutors. Dropbox and Cananical, company behind Ubuntu,  and other companies are using Rust. Firefox is porting its core components from C++ to Rust.


## Conclusion

Rust preserves the conveniences of high-level languages in low-level land. It's as fast as C/C++, and as safe and easy to use as higher-level lanaguages like Python/Ruby or Haskell.

Ref:

- https://medium.com/@Aimeedeer/why-rust-c877fba0ca94
- https://www.youtube.com/watch?v=cDFSrVhnZKo
- https://www.youtube.com/watch?v=_jMSrMex6R0&t=677s
- https://www.youtube.com/watch?v=-Tj8Q12DaEQ
- http://intorust.com/tutorial/why-rust/
