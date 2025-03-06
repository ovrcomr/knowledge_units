String slices as you might imagine, are specific to strings. But there's a more general slice type too.
Consider this array :

```rust
let a = [1, 2, 3, 4, 5];
```

Just as we might want to refer to part of a string, we might want to refer to a part of an array. We would do so
like this :

```rust
let array = [1, 2, 3, 4, 5];
let slice = &array[1..3];
assert_eq!(slice, &[2, 3]);
```

This slice has the type `&[i32]`. It works the same way as string slices do, by storing a reference to the
first element and a length. This kind of slice are used for all sorts of other collections.
