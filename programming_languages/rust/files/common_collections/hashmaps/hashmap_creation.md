**Hashmaps**

<br>

The type `HashMap<K, V>` stores a mapping of keys of type`K` to values of type `V` using a *hashing function*,
which dtermines how it places these keys and values into memory. Many programming languages support this kind
of data structure, but they often use a different name, such as *hash*, *map*, *hash table*, *dictionary* or
*associative array*, just to name a few.

Hash maps are useful when we want to look up data not by using index, as we can with vectors, but by using a
key that can be of any type. For example, in a game, we could keep track of each team's score in a hash map
in which each key is a team's name and the values are each team's score. Given a team name, we can retrieve its
score.

We'll go over the basic API of hash maps in this section but many more things are hiding in the functions defined
on `HashMap<K, V>` by the standard library. (Check the std lib for more informations)

<br>

---

<br>

**HashMap creation**

<br>

One way to ceate an empty hash map is to use `new()` and to add elements with `insert` :

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Blue"), 50);
```

Not that we need to first `use` the `HashMap` from the collections portion of the standard library.
Of our three common collections, this one is the least often used, so it's not included in the features
brought into scope automatically in the prelude. Hash maps also have less support from the standard library.
There is no built-in macro to construct them.

Just like vectors, hash maps store their data on the heap. This `HashMap` has keys of type `String` and values of
type `i32`. Like vectors, hash maps are homogeneous: all of the keys must have the same type, and all the value
must have the same type.
