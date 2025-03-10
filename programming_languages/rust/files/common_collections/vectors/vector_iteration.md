**Iterate through vectors**

<br>

To access each element of a vector in turn, we would iterate through all of the elements rather than use indices
to access one at a time :

```rust
let v = vec![100, 32, 57];
for item in &v {
    println!("{item}");
}
```

We can also iterate over mutable references to each element in a mutable vector in order to make changes to all
the elements :

```rust
let mut v = vec![100, 32, 57];
for item in &mut v {
    *i += 50;
}
```

To change the value that the mutable reference refers to, we have to use the `*` dereference operator to get to
the value in `item` before we can use the `+=` operator.

Iterating over a vector, whether immutably or mutably, is safe because of the borrow checker's rules. If we
attempt to insert or remove items in the `for` body, we would get a compiler error. The reference to the vector
that the `for` loop holds prevents simultaneous modifications of the whole vector.
