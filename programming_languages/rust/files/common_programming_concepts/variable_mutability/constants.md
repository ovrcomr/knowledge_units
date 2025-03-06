In Rust, variables are *immutable* by default :

```rust
fn main() {

    let x = 10;
    println!("The variable is equal to : {x}");

    x = 5;
    println!("The variable is equal to : {x}");
}
```

This program will have a compiling error, since the code tries to reassign `x`, that is *immutable* by nature.

<br>

---

<br>

In some cases, *mutable* variables can be needed, and can be created using `mut` :

```rust
fn main() {

    let mut x = 10; // x is now mutable and can be manipulated
    println!("The variable is equal to : {x}");

    x = 5;
    println!("The variable is equal to : {x}");
}
```

<br>

---

<br>

A variable can be *constant*, they are life-time *immutable* and cannot be set as mutable in any way (even with `mut`).
- The `const` keyword is used (instead of `let`),
- The name of the variable is written in uppercase by convention
- The type cannot be infered, so must be specified
- May be set only to a constant expression, not the result of a value that can only be computed at runtime.

```rust
const HOURS_IN_A_DAY: i32 = 24;
```

They are used for values that are not suposed to change any-time soon, such as the light-speed.
They are valid for the entire time a program runs, within the scope they were declared (useful for values that the whole program may need to know about).
Hardcoded values is useful in maintenance cases : there will be only one declaration to update.
