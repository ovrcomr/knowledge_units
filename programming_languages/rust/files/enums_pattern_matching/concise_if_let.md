The `if let` syntax lets combine `if` and `let` into a less verbose way to handle values that match one pattern while ingnoring the rest.

```rust
let config_max = Some(3u8); // Some(3u8) means "an Option<u8> that contains the value 3."

match config_max {
    Some(max) => println!("The maximum is configured to be {max}"),
    _ => (),
}
```

If the value is `Some`, we print out the value in the `Some` variant by binding the value to `max` in the pattern.
We don't want to do anything with the `None` value. To satisfy the `match` expression, we add `- => ()` after
processing just one variant which may be annoying to add.

Instead we could write this in a shorter way using `if let`. The following code behaves the same as the last one :

```rust
let config_max = Some(3u8);

if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}
```

`if let` simplifies pattern matching by combining a pattern and an expression with `=`. It works like `match`, where the pattern is the first arm.
For example, `Some(max)` extracts the value inside `Some`, allowing `max` to be used in the block, which runs only if the value matches.
This reduces typing, indentation, and boilerplate but removes match's exhaustive checking. Choosing between them depends on whether conciseness outweighs the need for full coverage.
Essentially, `if let` is syntactic sugar for a `match` that runs code for one pattern while ignoring others.

Adding `else` works like `_` in match. For instance, in the `Coin` enum, `if let` can count non-quarter coins while announcing quarters, just like match :

```rust
let mut count = 0;

match coin {
    Coin::Quarter(state) => println!("State quarter from {state:?}!"),
    _ => count += 1,
}

// Or with if let

let mut count = 0;

if let Coin::Quarter(state) = coin {
    println!("State quarter from {state:?}!");
} else {
    count += 1;
}
```

---

One common pattern is to perform some computation when a value is present and return a default value otherwise. Continuing on with our example of coins with a `UsState` value.
If we wanted to say something depending on how old the state on the quarter was, we might introduce a method on `UsState` to check the age of a state :

```rust
impl UsState {
    fn existed_in(&self, year: u16) -> bool {
        match self {
            UsState::Alabama => year >= 1819,
            UsState::Alaska => year >= 1959,
            // -- snip --
        }
    }
}
```

Then we might use `if let` to match on the type of coin, introducing a `state` variable within the body of the condition :

```rust
fn describe_state_quarter(coin: Coin) -> Option<String> {
    if let Coin::Quarter(state) = coin {
        if state.existed_in(1900) {
            Some(format!("{state:?} is old."))
        } else {
            Some(format!("{state:?} is relatively new."))
        }
    } else {
        None
    }
}
```

That gets the job done, but it has pushed the work into the body of the `if let` statement, and if the work to be done is more complicated,
it might be hard to follow exactly how the top-level branches relate. We could also take advantage of the fact that expressions produce a
value either to produce the `state` from the `if let` or to return early :

```rust
fn describe_state_quarter(coin: Coin) -> Option<String> {
    let state = if let Coin::Quarter(state) = coin {
        state
    } else {
        return None;
    };

    if state.existed_in(1900) {
        Some(format!("{state:?} is old."))
    } else {
        Some(format!("{state:?} is relatively new."))
    }
}
```

One branch of the if let produces a value, and the other one returns from the function entirely.

To make this common pattern nicer to express, Rust has `let-else`. The `let-else` syntax takes a pattern on the left side and an expression on the right,
very similar to `if let`, but it does not have an if branch, only an else branch. If the pattern matches, it will bind the value from the pattern in the
outer scope. If the pattern does not match, the program will flow into the `else` arm, which must return from the function.

```rust
fn describe_state_quarter(coin: Coin) -> Option<String> {
    let Coin::Quarter(state) = coin else {
        return None;
    };

    if state.existed_in(1900) {
        Some(format!("{state:?} is pretty old, for America!"))
    } else {
        Some(format!("{state:?} is relatively new."))
    }
}
```

If we have a situation in which the program has logic that is too verbose to express using a match, remember that `if let` and `let else` are in your Rust toolbox as well.
