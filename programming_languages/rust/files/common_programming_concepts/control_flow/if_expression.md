**Control flow** is the ability to run code based on a condition.
To create a conditon, values that are compared must be the same type.

<br>

---

<br>

**if** expression allows to branch code depending on a condition.
If the specified condition is `true`, then execute this block of code, if not, execute the other one.

```rust
let number: i32 = 10;

if number > 5 {
    println!("Condition is true"); // If greater
} else {
    println!("Condition is false"); // If smaller or equal to 5
}
```

The **else** expression is optional. If there is no `else` it will continue bellow.
A condition always evaluate to a `boolean` value, either `true` or `false`.

The `!` is used to revert a bollean value, or revert a condition (negation) :

```rust
let number = 10;

if number != 0 { // Instead of writing (if number < 0 || number > 0)
    print("number is not equal to 0");
}
```

<br>

---

<br>

**Multi-condition hanlding**

```rust
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
```

A control flow statement can be composed of :
- At least (and most) one `if`
- An infinite number of `else if`
- At most one `else`

<br>

---

<br>

**If in let statements**

Because `if` is an expression, it is possible to use it on the right side of a `let` statement to assign the outcome to a variable :

```rust
let condition: bool = true;
let number: i32 = if condition { 5 } else { 6 };
println!("Number is {number}");
```

The `number` variable will be bound to a value based on the outcome of the `if` expression.
