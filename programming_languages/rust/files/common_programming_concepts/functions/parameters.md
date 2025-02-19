Functions are prevalent in Rust code.
The `main` function is the entry point of many program.
The `fn` keyword used to declare a new function.

Rust code uses *snake_case* as the conventional style for functions and variables names.

```rust
fn main() {

    println!("Hello, world!");
    another_function();

}

fn another_function() {
    println!("Another function!");
}
```

Rust functions are defined by entering the `fn` keyword, following by the `function_name`, a pair of braces `()` for potential parameter(s), and curly braces `{}`
where the content of the function is written (where it begins and ends).

To call a function, type the name of the function, followed by a set of braces : `function_name();`

Functions can be defined either *bellow* or *above* the `main` function. Here, Rust only check the scope they are defined in.

---

**Parameters**

Functions can be designed to use *parameters* (also called arguments), that will bring more context to it.

```rust
fn main() {

    print_number(5); // The number is : 5
    print_number(190) // The numbe is : 190

}

fn print_number(x: i32) {
    println!("The number is : {x}")
}
```

The newly created `print_number()` created will print any number passed during the function call.
What is happening is that when the function is called with a number, the function will assign this value to the `x` parameter.
`x` have now the value of the given number. And the next step of the function is to print `x`, so it will print the value assigned to it.

In function *signature*, parameters types *must* be declared. The compiler will be able to give more helpful error messages if it knows what types the functions expects.

To define multiple parameter within a single function, separate them using commas :

```rust
fn some_function(value: i32, grade: char) { // param_name: param_type
    // Content of the function
}
```
