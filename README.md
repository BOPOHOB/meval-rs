[![Build Status](https://travis-ci.org/rekka/meval-rs.svg?branch=master)](https://travis-ci.org/rekka/meval-rs)
[![](http://meritbadge.herokuapp.com/meval)](https://crates.io/crates/meval)
[![meval at docs.rs](https://docs.rs/meval/badge.svg)](https://docs.rs/meval)

# meval

Just usual [meval](https://github.com/rekka/meval-rs) but with time computation future

## Documentation

- [Original meval full API documentation](https://docs.rs/meval)
- The difference between it is additional function Expr::eval_with_unit with return additional information about secons degree in a diven expression (see example),

## Simple examples

```rust
extern crate meval;

fn main() {
    let r = meval::eval_str("2:06:35.1 / 42.195 / 3:00").unwrap();

    println!("2:06:35.1 / 42.195 / 3:00 = {}", r);
}
```

If you need to know the measute of result value

```rust
extern crate meval;

use std::str::FromStr;
use meval::{ Expr, Error };

pub fn eval_str<S: AsRef<str>>(expr: S) -> Result<(f64, f64), Error> {
    let expr = Expr::from_str(expr.as_ref())?;
    expr.eval_with_unit()
}

pub fn sweet_eval<S: AsRef<str>>(expr: S) -> Result<String, Error> {
    let (result, degree) = eval_str(expr)?;

    let rounded = (result * 1000.0).round() / 1000.0;
    if degree == 1. {
        let sign = if rounded > 0.0 { "" } else { "-" };
        let mut seconds = rounded.abs();
        let hours = (seconds / 3600.0).floor() as i64;
        seconds -= (hours * 3600) as f64;
        let minutes = (seconds / 60.0).floor() as i64;
        seconds -= (minutes * 60) as f64;
        Ok(format!("{}{}:{:02}:{:07.4}", sign, hours, minutes, seconds))
    } else {
        Ok(format!("{}", rounded))
    }
}

fn main() {
    println!("The marathon pase time with pase 3:08 per kilometer is {}", sweet_eval("42.195 * 3:08").unwrap());

    let (result, degree) = eval_str("10000 * 2 / 1:17^2").unwrap();
    assert_eq!(degree, -2.0);
    println!("The acceleration of something is {}m/c^2", result);
}

```
