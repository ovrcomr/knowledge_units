It's possible to declare a variable within the same name as a previously created one.
The process is called *shadowing*, a sort of reassignation, meaning that the compiler will take in consideration the last statement of a variable :

```rust
let x = 5;
let x = x + 1; // x is shadowed and is now equal to 6
```

That is not the same as doing :

```rust
let x = 5;
x = x + 1;
```

In the first example, a 'new' variable is created and shadows the first one that had the same name, that is not the same as performing reassignation like
in the second example (that will throw an error).

---

Another illustrative example with different scopes :

```rust
fn main() {

    let x = 5;
    let x = x + 1;

    {
        let x = 10;
        println!("In this smaller scope, x = {x}");
    };

    println!("In this bigger scope, x = {x}");
}

// Output
// In this smallerscope, x = 10
// In this bigger scope, x = 6
```

---

By shadowing, it is also possible to change type from on declaration to the next one.

```rust
let spaces = "     "; // string
let spaces = spaces.len(); // integer
```

But for `mut` variables, it is not possible to change during reassignation :

```rust
let mut spaces = "    ";
spaces = spaces.len() // Attempting to reassing a number inside a string type variable (ERROR)
```
