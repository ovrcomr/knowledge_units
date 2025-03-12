**Accessing values in HashMap**

<br>

We can get a value out of the hash map by providing its key to the `get` method :

<br>

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

let team_name = String::from("Blue");
let score = scores.get(&team_name).copied().unwrap_or(0);
```

<br>

Here, `score` will have the value that is associated with the Blue team, and the result will be `10`.
The `get` method returns an `Option<&V>`; if there is no value for that key in the hash map, `get` will
return `None`. This program handles the `Option` by calling `copied` to get an `Option<i32>` rather than
an `Option<&i32>`, then `unwrap_or` to set `score` to zero if `scores` doesn't have an entrey for the key.

We can iterate over each key-value pair in hash map in a similar manner as we do with the vectors, using `for` :

<br>

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

for (key, value) in &scores {
    println!("{key}: {value}");
}

// Yellow: 50
// Blue: 10
```
