Control flow is the ability to run code based on a condition. In both cases it will perform some task.

The **if-expression** allows to branch code depending on a condition.
If the specified condition is `true`, then execute this block of code, if not, execute the other one.

```rust
fn main() {
    let number: i32 = 10;

    if number > 5 {
        println!("Condition is true");
    } else {
        println!("Condition is false");
    }
}
```

In both case, something will execute, and this something depends on the condition. Here it is if `number > 5`.
In the code, the condition is `true`, because `number = 10` and `10 > 5`, so the code inside the `if` expression will be executed.
In the case where `number` would be smaller, the executed block of code would be the `else` one.

The `else` expression is optional. If the condition specified in a single `if` expression is `false`, it will continue above, ignoring what is inside the `if` :

```rust
fn main() {
    let number: i32 = 10;

    if number < 7 {
        println!("Condition is true"); // This will not run because number is greater that 7
    }
}
```

Based on the format of the `boolean` type, a condition is alaways a `boolean` value. Either `true` or `false` :

```rust
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```

This will not work since `number` itself do not represent a `boolean`-like expresssion (and value). But `number > x` is,
because this expression is either `true` or `false`. Rust will not try to convert a provided condition in a `boolean` value as JavaScript or Ruby.
Being explicit is required to make it work.

It is possible to make a block of code run only when a number is not equal to 0, for example by using the `!` negation :

```rust
fn main() {

    let number = 10;

    if number != 0 {
        print("number is not equal to 0");
    }
}
```

A `boolean` preceeded by a `!` will revert is value : `!true = false` and `!false = true`.


---

**Multi-condition hanlding**

```rust
fn main() {

    let number: i32 = 6;

    if number % 4 {
        println!("This number is divisible by 4");
    } else if number % 3 {
        println!("This number is divisilbe by 3");
    } else if number % 2 {
        println!("This number is divisible by 2");
    } else {
        println!("This number is not divisible by 4, 3 and 2");
    }

}
```

A control flow statement can be composed of first `if` expression, then `x` `else if` expression(s) to handle three or more cases, and the the `else` expression to end.

---

**If in let statements**

Because `if` is an expression, it is possible to use it on the right side of a `let` statement to assign the outcome to a variable :

```rust
fn main() {

    let condition: bool = true;
    let number: i32 = if condition { 5 } else { 6 };

    println!("Number is {number}");

}
```

The `number` variable will be bound to a value based on the outcome of the `if` expression.
Because `number` is an integer, the mutliple case values that can be assigned to it must be integer to.
