It is often useful to create a new instance of a struct that includes most of the values
from the other instance, but changes some. It is possible to do so using *struct update syntax*.

Without the update syntax, creating `user2` using some of `user1` data :

```rust
fn main() {
    // --snip--

    let user2 = User {
        active: user1.active,
        username: user1.username,
        email: String::from("another@example.com"),
        sign_in_count: user1.sign_in_count,
    };
}
```

With the update syntax :

```rust
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

Fields that differs from the instance we use to create the other from needs to be
explicitly mentioned, but those who remains the same can be induced. `user2` have a
different `email` from the `user1` (used instance to create the other one), but every other
fields remains the same as in `user1`.

Note that the struct update syntax uses `=` like an assignment; this is because it moves the
data, just as we saw in [here](../../understanding_ownership/what_is_ownership/memory_allocation.md).
In this example, we can no longer use `user1` as a whole after creating `user2` because the
`String` in the username filed of `user1` was moved into `user2`. If we had given `user2` new
`String` values for both `email` and `username`, and thus only used the `active` and
`sing_in_count` values from `user1`, then `user1` would still be valid after creating `user2`.
Both `active` and `sign_in_count` are types that implement the *Copy* trait, so the behavior we
discussed in the “Stack-Only Data: Copy” section would apply. We can still use `user1.email`
in this example, since its value was not moved out.
