**String slicing**

<br>

Indexing into a string is often a bad idea because it is not clear what the return type of the string-indexing
operation should be : a byte value, a character, a grapheme cluster, or a string slice. If we really need to
use indices to create string slices, therefore, Rust asks us to be more specific.

Rather that indexing using `[]` with a single number, we can use `[]` with a range to create a string slice
containing particular bytes :

```rust
let hello = "Здравствуйте";
let extract = &hello[0..4];
```

Here, `extract` will be a `&str` that contains the first four bytes of the string. We mentionned that each
of these characters was two bytes, which means `extract` will be `Зд`.

If we were to try to slice only part of a character's byte with something like `&hello[0..1]`, Rust would
panic at runtime in the same way as if an invalid index were accessed in a vector.
The range `&hello[0..1]` is a problem since the range will the number before the specifyied one, maaking it
equivalent to writing `&hello[0]`, that caused problem too.

We should use caution when creating string slices ranges, because doing so can crash the program.
