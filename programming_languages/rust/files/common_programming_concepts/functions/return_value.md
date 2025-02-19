Functions can return values to the code that calls them.
Return values are not named, but must their type must be declared after an arrow (->).
In Rust, the return value of the function is synonymous with the value of the final expression in the block of the body of a function.
It is possible to return early from a function by using the `return` keyword and specifiying a value, but most functions return the last expression implicitly.
There is an example of a function that returns a value :

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();
    println!("x is equal to : {x}")
}
```

The type of the returned value is specified at the beginning of the function, and it will return the last expression of the function.

```rust
fn add_one(x: i32) -> i32 {
    x + 1
}

fn main() {
    let x = add_one(5);
    println!("x is equal to : {x}");
}
```

This works because the line inside the `add_one()` function is considered as an expression. In the case a semicolon is used, it will be a statement
and returns a error because of returning nothing. The compiler expect from the `add_one()` function to return something with the `i32` type, add the second case,
it will return nothing, `()` (unit type) instead of `i32`, that will cause an error.
