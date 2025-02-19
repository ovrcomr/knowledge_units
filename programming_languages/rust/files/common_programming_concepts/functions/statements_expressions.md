Functions bodies are made up of a series of statement optionally ending in an expression. So far,
the covered functions haven't included an ending expression, but expression as part of a statement have been seen.
Because Rust is an expression-based language, this in an important distinction to understand. Other languages don't have the same
distinctions. There is what expressions and statements are and how their differences affect the bodies of functions :

- Satements are instructions that perform some action and do not return a value.
- Expressions evaluate to a resultant value.

Creating a variable and assigning a value to it with the `let` keyword is a statement :

```rust
fn main() {
    let x: i32 = 5;
}
```

Function definitions are also *statements*; the entire preceding example is a *statement* in itself.
*Statements* do not return values. Therefore, it is not possible to assign a `let` *statement* to another variable, as
the following code tries to do :

```rust
fn main() {
    let x = (let y = 6); // This will throw an error
}
```

The *statement* `let y = 6` does not return anything, that's why it is impossible to bind it with a *statement*. This is different from languages like C or Ruby,
where the assignement returns the value of the assignment. In those languages, it is allowed to write `x = y = 6` and have both `x` and `y` have the value of `6`.

*Expressions* evaluate to a value and make up most of the rest of the code that will be written in Rust.
Let's consider the following math operation : `5+6` which is a *expression* that evaluates to `11`. *Expressions* can be part of a *statements*.
*Expressions* do not ends with semicolon.
