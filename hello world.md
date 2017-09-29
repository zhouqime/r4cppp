# Introduction - hello world!
# 介绍 - 你好，世界

If you are using C or C++, it is probably because you have to - either you need
low-level access to the system, or need every last drop of performance, or both.
Rust aims to offer the same level of abstraction around memory, the same
performance, but be safer and make you more productive.

如果你正在使用 C 或 C++ 语言，极有可能是因为你不得不使用——要么是因为你需要访问系统底层，要么是
你需要榨干最后一滴系统性能，在要么就是两者都有。Rust 语言的目标是：在提供相同内存抽象层次、相同
性能的情况下，提供更安全、更有创造力的语言。

Concretely, there are many languages out there that you might prefer to use to
C++: Java, Scala, Haskell, Python, and so forth, but you can't because either
the level of abstraction is too high (you don't get direct access to memory,
you are forced to use garbage collection, etc.), or there are performance issues
(either performance is unpredictable or it's simply not fast enough). Rust does
not force you to use garbage collection, and as in C++, you get raw pointers to
memory to play with. Rust subscribes to the 'pay for what you use' philosophy of
C++. If you don't use a feature, then you don't pay any performance overhead for
its existence. Furthermore, all language features in Rust have a predictable (and
usually small) cost.

具体而言，比起C++你可能更喜欢用如 Java, Scala, Haskell, Python 之类的其他语言，但是要么是因
为抽象层次太高（例如无法直接访问内存、被强制使用自动垃圾收集等等），要么是因为存在性能问题（例如性
能无法预测或者单纯的是不够快），你没办法使用这些语言。Rust不会强制你使用自动垃圾收集，同时如C++一
样，你可以直接操作内存的裸指针。Rust认同C++中“仅为使用到的特性买单”的哲学。如果你没有用到某个特性，
你就不必为之付出任何性能开销。而且，Rust的所有语言特性都有可预测（通常也很小）的开销。

Whilst these constraints make Rust a (rare) viable alternative to C++, Rust also
has benefits: it is memory safe - Rust's type system ensures that you don't get
the kind of memory errors which are common in C++ - memory leaks, accessing un-
initialised memory, dangling pointers - all are impossible in Rust. Furthermore,
whenever other constraints allow, Rust strives to prevent other safety issues
too - for example, all array indexing is bounds checked (of course, if you want
to avoid the cost, you can (at the expense of safety) - Rust allows you to do
this in unsafe blocks, along with many other unsafe things. Crucially, Rust
ensures that unsafety in unsafe blocks stays in unsafe blocks and can't affect
the rest of your program). Finally, Rust takes many concepts from modern
programming languages and introduces them to the systems language space.
Hopefully, that makes programming in Rust more productive, efficient, and
enjoyable.

这些约束使得Rust有望成功地（同时也是罕见地）成为一门C++的替代语言，与此次同时Rust也有自己的优点：
内存安全——Rust的类型系统能够确保你不会犯c++中的各种内存错误，内存泄漏、访问未经初始化的内存、
野指针等等错误都不会在Rust中发生。而且，当加入一些额外的约束时，Rust会尽量阻止其他安全问题——
例如，通常数组索引会做越界检查（当然，如果你希望避免检查开销，也是可以实现的（代价是安全性）—— Rust
允许你在非安全（unsafe）区块写包括这个在内的很多非安全代码。至关重要的是，Rust确保非安全代码只能
在非安全区块中存在，并且不会影响程序的其他部分）。最后，Rust把大量的现代编程语言中的概念引入系统编程
语言领域，希望这些概念能够使Rust编程变得更加高产、高效且有趣。

In the rest of this section we'll download and install Rust, create a minimal
Cargo project, and implement Hello World.

在本节剩余的部分我们将下载并安装Rust，创建一个最小的Cargo工程，并且实现“Hello World”。

## Getting Rust

You can get Rust from [http://www.rust-lang.org/install.html](http://www.rust-lang.org/install.html).
The downloads from there include the Rust compiler, standard libraries, and
Cargo, which is a package manager and build tool for Rust.

你能够从[http://www.rust-lang.org/install.html](http://www.rust-lang.org/install.html)
获取Rust，包括Rust语言的编译器、标准库以及Cargo——Rust的包管理与构建工具。

Rust is available on three channels: stable, beta, and nightly. Rust works on a
rapid-release, schedule with new releases every six weeks. On the release date,
nightly becomes beta and beta becomes stable.

Rust提供3种版本：稳定版（stable）、公测版（beta）以及开发版（nightly）。Rust语言采用敏捷发布，
按计划每6周发布新版。当新版发布时，开发版成为公测版，公测版成为稳定版。

Nightly is updated every night and is ideal for users who want to experiment with
cutting edge features and ensure that their libraries will work with future Rust.

开发版每天晚上都会更新，适合想体验尖端特征同时兼容未来Rust的开发者。

Stable is the right choice for most users. Rust's stability guarantees only
apply to the stable channel.

稳定版对于大部分开发者来说都是正确的选择。Rust的稳定性保证仅仅在稳定版本适用。

Beta is designed to mostly be used in users' CI to check that there code will
continue to work as expected.

So, you probably want the stable channel. If you're on Linux or OS X, the
easiest way to get it is to run

```
curl -sSf https://static.rust-lang.org/rustup.sh | sh
```

On Windows, a similarly easy way would be to run

```
choco install rust
```

For other ways to install, see [http://www.rust-lang.org/install.html](http://www.rust-lang.org/install.html).

You can find the source at [github.com/rust-lang/rust](https://github.com/rust-lang/rust).
To build the compiler, run `./configure && make rustc`. See
[building-from-source](https://github.com/rust-lang/rust#building-from-source)
for more detailed instructions.


## Hello World!

The easiest and most common way to build Rust programs is to use Cargo. To start
a project called `hello` using Cargo, run `cargo new --bin hello`. This will
create a new directory called `hello` inside which is a `Cargo.toml` file and
a `src` directory with a file called `main.rs`.

`Cargo.toml` defines dependencies and other metadata about our project. We'll
come back to it in detail later.

All our source code will go in the `src` directory. `main.rs` already contains
a Hello World program. It looks like this:

```rust
fn main() {
    println!("Hello, world!");
}
```

To build the program, run `cargo build`. To build and run it, `cargo run`. If
you do the latter, you should be greeted in the console. Success!

Cargo will have made a `target` directory and put the executable in there.

If you want to use the compiler directly you can run `rustc src/hello.rs` which
will create an executable called `hello`. See `rustc --help` for lots of
options.

OK, back to the code. A few interesting points - we use `fn` to define a
function or method. `main()` is the default entry point for our programs (we'll
leave program args for later). There are no separate declarations or header
files as with C++. `println!` is Rust's equivalent of printf. The `!` means that
it is a macro. A subset of the standard library is available without needing to
be explicitly imported/included (the prelude). The `println!` macro is included
as part of that subset.

Lets change our example a little bit:

```rust
fn main() {
    let world = "world";
    println!("Hello {}!", world);
}
```

`let` is used to introduce a variable, world is the variable name and it is a
string (technically the type is `&'static str`, but more on that later). We
don't need to specify the type, it will be inferred for us.

Using `{}` in the `println!` statement is like using `%s` in printf. In fact, it
is a bit more general than that because Rust will try to convert the variable to
a string if it is not one already<sup>[1](#1)</sup> (like `operator<<()` in C++).
You can easily play around with this sort of thing - try multiple strings and
using numbers (integer and float literals will work).

If you like, you can explicitly give the type of `world`:

```rust
let world: &'static str = "world";
```

In C++ we write `T x` to declare a variable `x` with type `T`. In Rust we write
`x: T`, whether in `let` statements or function signatures, etc. Mostly we omit
explicit types in `let` statements, but they are required for function
arguments. Lets add another function to see it work:

```rust
fn foo(_x: &'static str) -> &'static str {
    "world"
}

fn main() {
    println!("Hello {}!", foo("bar"));
}
```

The function `foo` has a single argument `_x` which is a string literal (we pass
it "bar" from `main`)<sup>[2](#2)</sup>.

The return type for a function is given after `->`. If the function doesn't
return anything (a void function in C++), we don't need to give a return type at
all (as in `main`). If you want to be super-explicit, you can write `-> ()`,
`()` is the void type in Rust.

You don't need the `return` keyword in Rust, if the last expression in a
function body (or any other block, we'll see more of this later) is not finished
with a semicolon, then it is the return value. So `foo` will return
"world". The `return` keyword still exists so we can do early returns. You can
replace `"world"` with `return "world";` and it will have the same effect.


## Why?

I would like to motivate some of the language features above. Local type
inference is convenient and useful without sacrificing safety or performance
(it's even in modern versions of C++ now). A minor convenience is that language
items are consistently denoted by keyword (`fn`, `let`, etc.), this makes
scanning by eye or by tools easier, in general the syntax of Rust is simpler and
more consistent than C++. The `println!` macro is safer than printf - the number
of arguments is statically checked against the number of 'holes' in the string
and the arguments are type checked. This means you can't make the printf
mistakes of printing memory as if it had a different type or addressing memory
further down the stack by mistake. These are fairly minor things, but I hope
they illustrate the philosophy behind the design of Rust.


##### 1

This is a programmer specified conversion which uses the `Display` trait, which
works a bit like `toString` in Java. You can also use `{:?}` which gives a
compiler generated representation which is sometimes useful for debugging. As
with printf, there are many other options.

##### 2

We don't actually use that argument in `foo`. Usually,
Rust will warn us about this. By prefixing the argument name with `_` we avoid
these warnings. In fact, we don't need to name the argument at all, we could
just use `_`.
