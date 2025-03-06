**Return value** can make functions, that are initialy *statements*, evaluate to something.
The *return value* is specified by :
- The `->`, meaning that the function returns something
- The type of the returned value (that must be specified)
- The return value evaluates to the last expression in the function content

```rust
fn add_one(x: i32) -> i32 {
    x + 1
}

fn main() {
    let x = add_one(5);
    println!("x is equal to : {x}");
}
```

In the case a function is not designed to return something, it will return the unit `()` type.
