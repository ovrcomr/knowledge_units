Comments are useful to annotate a program, make it more readable and improve separation of concerns.
Everything written within a comment will be ignored by the compiler, meaning that it is possible to write text
inside code, to add reminders, facts, questions, structure or whatever useful, right inside the code, without breaking it.

In Rust, single-line comments are starts with a double slash :

```rust
// This is the beggining of the program (aslo a comment)

fn main() {
    // The content of the main function is under development
    // The steps remains :
    // 1. Create ...
    // 2. Add to it ...
    // 3. Return the result
    // 4. Print the result
}
```

They can also be placed next to or above a line as here :

```rust
// Start of the main function
fn main() {

    // Create a variable
    let x = 10; // Immutable variable x equals to 10
    // Print this variable
    println!("{x}") // Print statement that display the variable created above

}
```

This is for example purpose, but comments should be used when necessary, not usually within a short and simple code as above.
