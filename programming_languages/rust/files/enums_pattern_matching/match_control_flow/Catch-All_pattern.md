Using enums, we can also take special actions for few particular cases, and create a default one for all the others.

```rust
let dice_roll = 9;

match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    other => move_player(other),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
```

For the first two arms, the patterns are the literal values `3` and `7`. For the last arm that covers every other possible value,
the pattern is the variable we’ve chosen to name other. The code that runs for the other arm uses the variable by passing it to
the move_player function.

This code compiles, even though we haven’t listed all the possible values a `u8` can have, because the last pattern will match all values not specifically listed.
This catch-all pattern meets the requirements that `match` must be exhaustive.
The `other` have to be place in last, because otherwise every single operation will match the `other` arm, and the following ones will not even be evaluated.

---

`_` is a special pattern that matches any value and does not bind to that value. This tells Rust we aren’t going to use the value, so Rust won’t warn us about an unused variable :

```rust
let dice_roll = 9;

match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => reroll(),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn reroll() {}
```

This example also meets the exhaustiveness requirement because we’re explicitly ignoring all other values in the last arm; we haven’t forgotten anything.

---

And what if we want nothing else happens on your turn if you roll anything other than a 3 or a 7 :

```rust
let dice_roll = 9;

match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => (),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
```

Here, we’re telling Rust explicitly that we aren’t going to use any other value that doesn’t match a pattern in an earlier arm, and we don’t want to run any code in this case.
