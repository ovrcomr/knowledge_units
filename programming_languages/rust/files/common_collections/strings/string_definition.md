**String definition**

<br>

We are discussing strings in the context of collections because strings are implemented as a collection of bytes,
plus ome methods to provide useful functionality when those bytes are interpreted as text. In this section,
we will talk about the operations on `String` that every collection type has, such has creating, updating and
reading. We will aslo discuss the ways in which `String` differs from the other collections, namely how indexing
into a `String` is complicated by the difference between how people and computers interpret `String` data.

<br>

Rust has only one string type in the core language, which is the string slice `str` that is usually seen
in borrowed from `&str`. String slices are references to some UTF-8 encoded string data stored elsewhere. String
literals, for example, are stored in the program's binary and are therefore string slices.

The `String` type, which is porvided by Rust's standard library rather that coded into the core language, is a
growable, mutable, owned, UTF-8 encoded string type. When developers talk about "strings" in Rust, they might
be referring ti either `String` or the string slice `&std` types, not just one of those types, and both
are UTF-8 encoded.
