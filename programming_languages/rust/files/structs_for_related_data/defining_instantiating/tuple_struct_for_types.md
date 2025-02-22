Rust also support structs that look similar to tuples, called *tuple structs*.
Tuples structs have the added meaning the struct name provides but don't have names
associated with their fields; rather, they just have the types of the fields.
Tuple structs are useful when you want to give the whole tuple a name and make the tuple
a diffrent type from the other tuples and, when naming each field as a regular struct would be
verbose or redundante.

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

`black` and `origin` values are different types because they are instances of diffrent tuple
structs. Each defined struct is its own type, even though the fields within the struct might
have the same types. For example, a function that takes a parameter of type `Color` cannot
take a `Point` as argument, even though both types are made of the same three `i32` values.
To access value from tuple structs, we must use the dot notation followed by the index of the
value we want to access :

```rust
struct Color(i32, i32, i32);

fn main() {
    let almost_black = Color(1, 2, 3);
    let first_value_of_almost_black = almost_black.1;
}
```

Unlike tuples, tuple structs require you to name the type of the struct when you destructure them.
For example, we would write `let Point(x, y, z) = point`.
