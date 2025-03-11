**Iterating over strings**

<br>

The best way to operate on piecees of strings is to be explicit about whether we want characters or bytes.
For individual Unicode scalar values, use the `chars` method. Calling `chars` on `Зд` separates out and returns
two values of type `char`, and we can iterate over the result to access each element :

```rust
for character in "Зд".chars() {
    println!("{character}")
}
```

Alternatively, the `bytes` method returns each raw byte, which might be appropriate for our domain :

```rust
for b in "Зд".bytes() {
    println!("{b}"); // 208 151 208 180
}
```

But be sure to remember that valid Unicode scalar values may be made up of more than one byte.

Getting grapheme clusters from strings, as with the Devanagari script, is complex, so this functionality is
not provided by the standard library. Crates are available on `crates.io` if this functionality is needed.
