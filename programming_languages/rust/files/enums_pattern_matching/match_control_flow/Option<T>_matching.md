In the previous section, we wanted to get the inner `T` value out of the `Some` case when using `Option<T>`.
We can also handle `Option<T>` using `match`, as we did in the `Coin` enum. Instead of comparing coins, we will compare
the variants of `Option<T>`, but the way the `match` expression works remains the same.

Let's write a function that takes an `Option<i32>` and, if there is a value inside, adds 1 to that value.
If there is not a value inside, the function should return the `None` value and not try to perform any opperations.

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

---

When we call `plus_one(five)`, the variable `x` in the body of `plus_one` will have the value `Some(5)`.
We then compare that against each match arm :

```rust
None => None,
```

The `Some(5)` does not match the pattern `None`, so we continue to the next arm :

```rust
Some(i) => Some(i + 1),
```

`Some(5)` does match `Some(i)`, we have the same variant. The `i` binds to the value contained in `Some`, so `i` takes the value `5`.
The code in the match arm is then executed, and returns a new `Some(i + 1)` expression that will be equal to `6` in this case.


---

When we call `plus_one(None)`, the variable `x` in the body of `plus_one` will have the value `None`.
We then compare that against each match arm :

```rust
None => None,
```

Because it matches, there is no value to add to, so the program stops and return `None`. on the right side of `=>`.
Because the first arm matched, no other arms are compared.
