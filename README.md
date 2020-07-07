[![Build Status](https://travis-ci.org/rekka/meval-rs.svg?branch=master)](https://travis-ci.org/rekka/meval-rs)
[![](http://meritbadge.herokuapp.com/meval)](https://crates.io/crates/meval)
[![meval at docs.rs](https://docs.rs/meval/badge.svg)](https://docs.rs/meval)

# meval

Just usual [meval](https://github.com/rekka/meval-rs) but with time computation future

## Documentation

- [Full API documentation](https://docs.rs/meval)

## Simple examples

```rust
extern crate meval;

fn main() {
    let r = meval::eval_str("2:06:35.1 / 42.195 / 3:00").unwrap();

    println!("2:06:35.1 / 42.195 / 3:00 = {}", r);
}
```

