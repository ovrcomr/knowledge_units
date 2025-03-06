*Shadowing* is the process of 'overwriting' an already-existing variable by naming another one as the previous :

```rust
let x = 5;
// From here x = 5
let x = x + 1; // From here x = 6
```

<br>

---

<br>

Another illustrative example with different scopes :

```rust
fn main() {

    let x = 5;
    println!("At first, x = {}", x);
    let x = x + 1;

    {
        let x = 10;
        println!("In this smaller scope, x = {x}");
    };

    println!("In this bigger scope, x = {x}");
}

// Output
// At first, x = 5
// In this smallerscope, x = 10
// In this bigger scope, x = 6
```

<br>

---

<br>

By shadowing, it is also possible to change type from on declaration to the next one.

```rust
let spaces = "     "; // string
let spaces = spaces.len(); // integer
```

Changing type is only possible when re-declaration (not for simple re-assignation).
