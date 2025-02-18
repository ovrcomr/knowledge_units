In Rust, variables are *immutable* by default, meaning that they can be retreived and used, but not modified.
For the following piece of code :

```rust
fn main() {

    let x = 10;
    println!("The variable is equal to : {x}");

    x = 5;
    println!("The variable is equal to : {x}");
}
```

This program will have a compiling error, since the code tries to reassign `x`, that is *immutable* by nature.

If one part of the code operates on the assumption that a value will never change and another part of the code changes that value,
it's possible that the first part of the code won't do what it was desinged to do. The cause of this kind of bug can be hard to track down,
especially when the second piece of code changes the value only sometimes.

The Rust compiler guarantees that a value is *immutable* by default, so the developer do not need to keep track of it over time.

But in some cases, the developer might need to have some *mutable* variables, and can do it using `mut` :

```rust
fn main() {

    let mut x = 10; // x is now mutable and can be manipulated
    println!("The variable is equal to : {x}");

    x = 5;
    println!("The variable is equal to : {x}");
}
```

---

Like *immutable* variables, *constants* are variable that are bound to a name and are not allowed to change, but there is few differences for constants :
- It is not possible to use `mut` for a constant variable, they are life-time immutable.
- Constants are declared using the `const` keyword (instead of `let`), and the type of the value must be specified.
- The naming convention of a constant is to write its name using uppercase and underscore between words.
- May be set only to a constant expression, not the result of a value that can only be computed at runtime.

```rust
const THREE_HOURS_IN_SECOND = 60 * 60 * 3;
```

Constants are valid for the entire time a program runs, within the scope they were declared in. It is useful for a value that the whole program may need
to know about, such as light speed. Naming hardcoded values is useful since if a future maintenance is needed, there will be only one decleration of the a
variable to update.
