**Hashing functions**

<br>

By default, `HashMap` uses a hashing function called *SipHash* that can provide resistance to denial-of-serviec
(DoS) attacks involving hash tables. This is the not fastest hashing algorithm available, but the trade-off
for better security that comes with the drop in performance is worth it. If we profile our code and find
that the default hash function is too slow for our purposes, we can switch to another function by specifying
a different hasher. A *hasher* is a type that implements the `BuildHasher` trait. We don't necessarly have to
implement our own hasher from scratch; crates.io has libraries shared by other Rust users that provide
hashers implementing many common hashing algorithms.
