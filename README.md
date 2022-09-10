# fallback

This is a helper library to implement fallback mechaism.
It contains two `Option`, and if the "desired" one is `None`, the "base" one will be chosen.

A trait called `FallbackSpec` is used to implement field fallback for a struct.

``` rust
use fallback::*;

#[derive(FallbackSpec)]
struct Foo {
    data1: i32,
    data2: String,
}

let data = Foo {
    data1: 123,
    data2: "Hello".to_string(),
};

let data = Fallback::new(None, Some(data));
let data = data.spec();

assert_eq!(data.data1.unzip(), (None, Some(123)));
assert_eq!(data.data2.unzip(), (None, Some("Hello".to_string())));
```
