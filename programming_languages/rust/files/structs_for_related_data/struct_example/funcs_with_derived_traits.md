It would be useful to be able to print an instance of `Rectangle` while we are debugging the
program and see the values for all its fields :

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {}", rect1);
}
```

When we compile this code, we get an error with this core message :

```bash
error[E0277]: `Rectangle` doesn't implement `std::fmt::Display`
```

The `println!()` macro can do many kinds of formatting, and by default, the curly braces tell
`println!()` to use formatting known as `Display` : output intended for direct end user
consumption. The primitive types we have seen so far implement `Display` by default because
there is only one way we would want to show a `1` or any other primitive type to a user.
But with structs, the way `println!` should format the output is less clear because there are
more display possibilities:  Is coma wanted or not ? Is curly braces wanted or not ?
Should all the fields be shown ? Due to this ambiguity, Rust doesn't try to guess what we want,
and structs don't have a provided implementation of `Display` to use with `println!` and the
`{}` placeholder.

If we contunie reading the errors, we will find the helpful note :

```bash
= help: the trait `std::fmt::Display` is not implemented for `Rectangle`
= note: in format strings you may be able to use `{:?}` (or {:#?} for pretty-print) instead
```

Rust *does* include functionality to print out debugging information, but we have to explicitly
opt in to make that functionality available for our struct. To do that, we add the outer
attribute `#[derive(Debug)]` just before the struct definition :

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {rect1:?}");
}
```

When running the program :

```bash
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle { width: 30, height: 50 }
```

Writing `println!("rect1 is {rect1:#?}"` using `:#?` will print the result is a slightly
different way :

```rust
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle {
    width: 30,
    height: 50,
}
```

---

Another way to print out a value using the `Debug` fromat is to use the `dbg! macro`
which takes ownership of an expression (as opposed to `println!` which takes a refrence),
prints the file and line number of where that `dbg!` macro call occurs in the code along
with the resultant value of that expression, and returns ownership of the value.

(When using `dbg!`, pass in a reference to avoid transfering ownership)

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

We can put `dbg!` around the expression `30 * scale` and, because `dbg!` returns ownership of the
expression’s value, the width field will get the same value as if we didn’t have the `dbg!`
call there. We don’t want `dbg!` to take ownership of `rect1`, so we use a reference to `rect1`
in the next call. Here’s what the output of this example looks like:

```rust
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.61s
     Running `target/debug/rectangles`
[src/main.rs:10:16] 30 * scale = 60
[src/main.rs:14:5] &rect1 = Rectangle {
    width: 60,
    height: 50,
}
```
