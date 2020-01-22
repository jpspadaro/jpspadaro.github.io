---
layout: post
title: Rustiness
---


# ![](https://www.rust-lang.org/static/images/rust-logo-blk.svg)ustiness

So after working with Go and working with Rust for a little bit, Rust has won out as far as what I focus on. Don't get me wrong, I love the `go` keyword for concurrency. It's nice to see it baked in like that.

**BUT...**

Frankly, Rust's speed is fantastic, it's support tools (`cargo`, `rls`, etc) are slick, and even though it's not baked in the same way, it's still stupid-simple:

```
use rayon::prelude::*;

(0..100).into_par_iter().for_each(|x| println!("{:?}", x));
```

*BAM.* Two lines and you have minimal fuss for a multi-threaded program. Want to use channels to pass data around? Here you go:

```
use std::sync::mpsc::channel;
use rayon::prelude::*;

let (sender, receiver) = channel();

(0..5).into_par_iter().for_each_with(sender, |s, x| s.send(x).unwrap());

let mut res: Vec<_> = receiver.iter().collect();

res.sort();

assert_eq!(&res[..], &[0, 1, 2, 3, 4])
```

Not too terrible. Add the Rust guarentees, and you've got a pretty safe, easy langauge for threads. I'm a fan.


***Note: Examples from [here](https://docs.rs/rayon/1.3.0/rayon/iter/trait.ParallelIterator.html) in the documentation.***
