A *dangling* pointer is are pointer that reference a location in memory that may
have been given to someone else by freeing some memory while preserving a pointer to that memory.
In Rust, by contrast, the compiler guarentess that references will never be dangling references.
If you have a reference to some data, the compiler will ensure that the data will not go out of
scope before the reference to the data does.

There is a attempt to cause a dangling pointer :

```rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```

The error message is the following :

```bash
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0106]: missing lifetime specifier
 --> src/main.rs:5:16
  |
5 | fn dangle() -> &String {
  |                ^ expected named lifetime parameter
  |
  = help: this function's return type contains a borrowed value, but there is no value for it to be borrowed from
help: consider using the `'static` lifetime, but this is uncommon unless you're returning a borrowed value from a `const` or a `static`
  |
5 | fn dangle() -> &'static String {
  |                 +++++++
help: instead, you are more likely to want to return an owned value
  |
5 - fn dangle() -> &String {
5 + fn dangle() -> String {
  |

error[E0515]: cannot return reference to local variable `s`
 --> src/main.rs:8:5
  |
8 |     &s
  |     ^^ returns a reference to data owned by the current function

Some errors have detailed explanations: E0106, E0515.
For more information about an error, try `rustc --explain E0106`.
error: could not compile `ownership` (bin "ownership") due to 2 previous errors
```

In `dangle()`, first, the `String::new()` is created and owned by `s`, then, a *reference* to `s` is created.
Until now, the *reference* accesses data exists, but once assignation time comes for
the `reference_to_nothing` variable in `main()`, the scope of `dangling()` ends, the data inside it is relieved,
and the *reference* is now dangling, before being assigned to `reference_to_nothing`.

The solution here is to return the `String` directly.
