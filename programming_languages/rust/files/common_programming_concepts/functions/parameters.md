**Functions** are prevalent in Rust code :
- `main()` function is the entry point of every program
- They are conventionaly named using *snake_case*
- They are available in the scope they are defined in

```rust
fn main() {

    println!("Hello, world!");
    another_function();

}

fn another_function() {
    println!("Another function!");
}
```

---

**Parameters**

They are used used to give more context to a function, they must have :
- An explicit *name* that helps understanding
- An associated *type* (mandatory)
- Separated by commas if more than one

```rust
fn main() {

    print_number(5); // The number is : 5
    print_number(190) // The numbe is : 190

}

fn print_number(x: i32) {
    println!("The number is : {x}")
}
```
