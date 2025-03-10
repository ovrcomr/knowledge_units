**Enums for multiple types**

<br>

Vectors can only store values that are of the same type. This can be inconvinient, there are definitely use cases
for needing to store a list of items of different types. The variants of an enum are defined under the same enum
type, so when we need on type to represent elements of different types, we can define and use an enum.

<br>

```rust
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```

<br>

Rust needs to know what types will be in the vector at compile time so it knows exactly how much memory on the
heap will need to be allocated to store each element. We must also be explicit about what types are allows in this
vector. If Rust allowed a vector to hold any type, there would be a chance that one or more of the types would cause
errors with the operations performed on the elements of the vector. Using an enum plus a `match` expression means
that Rust will ensure at compile time that every possible case is handled.

(There is another way to do that with trait object, that will be covered later)
