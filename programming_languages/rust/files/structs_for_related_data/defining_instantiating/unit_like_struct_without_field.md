We can also define structs that do not have any fields. These are called *unit-like structs*
because they behave similarly to `()`, the unit type. Un-like structs can be useful when we need to
implement a trait on some type but do not have any data that we want to store in the type itself.

```rust
struct AlwayasEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

To define `AlwaysEqual`, we use the `struct` keyword, the name we want, and then a semicolon. No
need for curly braces or braces. Then we can gat an instance of `AlwaysEqual` in the `subject`
variable in a similar way: using the name we defined, without any curly braces or braces.

---

**Ownership of struct data**

In the `User` struct definition, we used the owned `String` type rather than the `&str`
string slice type. This is a deliberate choice because we want each instance of this struct to own
all of its data and for that data to be valid for as long as the entire struct is valid.

It is also possible for structs to store references to data owned by something else, but to do
so requires the use of lifetimes, a Rust feature that we’ll discuss in Chapter 10. Lifetimes
ensure that the data referenced by a struct is valid for as long as the struct is. Let’s say
you try to store a reference in a struct without specifying lifetimes, like the following;
this won’t work:

```rust
struct User {
    active: bool,
    username: &str,
    email: &str,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        active: true,
        username: "someusername123",
        email: "someone@example.com",
        sign_in_count: 1,
    }
}
```

The compiler will complain that needs lifetime specifiers :

```bash
$ cargo run
   Compiling structs v0.1.0 (file:///projects/structs)
error[E0106]: missing lifetime specifier
 --> src/main.rs:3:15
  |
3 |     username: &str,
  |               ^ expected named lifetime parameter
  |
help: consider introducing a named lifetime parameter
  |
1 ~ struct User<'a> {
2 |     active: bool,
3 ~     username: &'a str,
  |

error[E0106]: missing lifetime specifier
 --> src/main.rs:4:12
  |
4 |     email: &str,
  |            ^ expected named lifetime parameter
  |
help: consider introducing a named lifetime parameter
  |
1 ~ struct User<'a> {
2 |     active: bool,
3 |     username: &str,
4 ~     email: &'a str,
  |

For more information about this error, try `rustc --explain E0106`.
error: could not compile `structs` (bin "structs") due to 2 previous errors
```

Storing references in struct will be discussed later on (chap 10).
