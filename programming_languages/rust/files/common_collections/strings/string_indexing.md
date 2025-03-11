**Indexing into Strings**

<br>

In many other programming languages, accessing individual characters in a string by referencing them by index is
a valid and common operation. However, if we try to access parts of a `String` using indexing syntax in Rust, it
will not work.

The error and the note tells that Rust doesn't not support string indexing, and to understand why;
we have to discuss about how Rust stores strings in memory.

<br>

*Internal representation*

A `String` is a wrapper over a `Vec<8>`. Let's look at some of our properly encoded UTF-8 example strings :

```rust
let hello = String::from("Hello");
```

In this case, `len` will be `4`, so 4 bytes long. Each of these letters takes one byte encoded in UTF-8.

```rust
let hello = String::from("Здравствуйте"); // len = 24 (24 bytes long)
```

That is because eahc Unicode scalar value in that string takes 2 bytes of storage. Therefore, an index
int the string's bytes will not always correlate to a valid Unicode scalar value :

```rust
let hello = "Здравствуйте";
let answer = &hello[0];
```

We already know that `answer` will not be `3` (the first letter). When encoded in UTF-8, the first byte of
`3` is `208` and the second is `151`, so it would seem that `answer` should in fact be `208`, but it is not a
valid character on its own. Returning `208` is likely not what the user would want if they asked for the first
letter if this string. However, that is the only data that Rust has the byte index `0`. Users generally dont' want
the byte value returned, even if the string contains only latin letters. If `&hello[0]` were valid code
that returned the byte value, it would return `104`, not `h`.

The answer, then, is that to avoid returning an unexpected value and causing bugs that might not be discovered
immediately, Rust doesn't compile this code at all and prevents misunderstanding early in the development process.

<br>

*Bytes and scalar values and grapheme clusters!*

Another point about UTF-8 is that there are actually three relevant ways to look at strings from
Rust's perspective : as bytes, scalar values, and grapheme clusters (the cloesest thing to what we
could call letter).

If we look at the Hindi word “नमस्ते” written in the Devanagari script, it is stored as a vector of u8
values that looks like this :

```rust
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164, 224, 165, 135]
```

That is 18 bytes and is how computers ultimately store this data. If we look at them as Unicode scalar values,
which are what Rust's `char` type is, those bytes look like this :

```rust
['न', 'म', 'स', '्', 'त', 'े']
```

There are six `char` values here, but the fourth and sixth are not letters: they are diacritics that don't make
sense on their own. Finally, if we look at them as grapheme clusters, we'd get what a person would call the
four letters that make up the Hindi word :

```rust
["न", "म", "स्", "ते"]
```

Rust provides different ways of interpreting the raw string data that computers store so that each program can
choose the interpretation it needs, no matter what human language the data is in.

A final reason Rust doesn't allow us to index into a `String`to get a character is that indexing operations are
expected to always take constant time (O(1)). But it is not possible to guarantee that performance with a `String`,
because Rust would have to walk through the contents from the beginning to the index to determine how many valid
characters there were.
