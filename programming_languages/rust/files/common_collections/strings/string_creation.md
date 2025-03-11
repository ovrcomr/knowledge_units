**String creation**

Many of the same operations available with the `Vec<T>` are available with `String` as well because `String`
is actually implemented as a wrapper around a vector of bytes with some extra guarentees, restrictions and
capabilities. An example of a function that works the same way with `Vec<T>` and `String` is the `new` function :

<br>

```rust
let mut new_string = String::new();
```

This line creates a new, empty string called `new_string`, into which we can then hold data. Often, we will have
some initial data which we want to start the string. For that, we use the `to_string` method, which is available
on any type that implement the `Display` trait, as string literals do :

```rust
let data = "initial content";
let data_string = data.to_string();
// let data_string = "initial content".to_string() alos works
```

We can also use the `String::from()` function to create a `String` from a string literal :

```rust
let message = String::from("Hello everyone");
```

<br>

Because strings are used for so many things, we can use many different generic API for strings, providing us with
a lot of options. Some of them can seem redudant, but they all have their place. In this case, `String::from()`
and `to_string` do the same thing, so which one we choose is a matter of style and readability.

Because strings are UTF-8 encoded, we can include any properly encoded data in them.
