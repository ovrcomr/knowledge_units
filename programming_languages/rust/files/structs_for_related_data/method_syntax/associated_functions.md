All functions defined within an `impl` block are called *associated functions* because they are associated with
the type named after the `impl`. We can define associated functions that do not have `self` as their first
parameter (and thus are not methods) because they do not need an instance of the type to work with.
We have already used one function like this: the `String::from()` function that is defined on the `String` type.

Associated functions that are not methods are often used for constructors that will return a new instance of the
struct. These are often called `new`, but `new` is not a special name and is not built into the language, it can
be seen as a naming convention.

```rust
impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```

Here, `square` is a constructor, that create a new instance of `Rectangle`.
It takes only one paramter since a square have same width and height.
To use this constructor to create a new instance :

```rust
let new_square: Rectangle = Rectangle::square(10);
```
