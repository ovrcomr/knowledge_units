**HashMap updating**

<br>

Although the number of key and value pairs is growable, each unique key can only have one value associated
with it at a time.

When we want to change the data in a hashmap, you have to decide how to handle the case when a key already
has a value assigned. We could replace the old value with the new value, completely disregarding the old value.
We could keep the old value and ignore the new value, only adding the new value. Or we could combine
the old value and the new value.

<br>

---

*Overwriting a value*

<br>

If we insert a key and a value into a hash map and then insert that same key with a different value, the value
associated with that key will be replaced. Even thought the code down below calls `insert` twice, the hash
map will only contain one key-value pair because we are inserting the value for the Blue teams' key both times :

<br>

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10); // Key : Blue
scores.insert(String::from("Blue"), 25); // Key : Blue

println!("{scores:?}");
```

<br>

*Adding a key and value only if a key isn't present*

<br>

It is common to check whether a particular key already exists in the hash map with a value and then to take
the following actions : if the key does exists in the hashmap, the existing value should remain the way it is;
if the key doesn't exist, insert it and a value for it.

Hashmaps have a special API for this called `entry` that takes they key you want to check as a parameter.
The return value of the `entry` method is an enum called `Entry` that represents a value that might or might not
exist. Let's say we want to check whether the key for the Yellow team has a value associated with it. If it doesn't
we want to insert the value `50`, and the same for the Blue team. Using the `entry` API, the code looks like :

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);

scores.entry(String::from("Yellow")).or_insert(50);
scores.entry(String::from("Blue")).or_insert(50);

println!("{scores:?}");
```

The `or_insert` method on `Entry` is defined to return a mutable reference to the value for the corresponding
`Entry` key if that key exists, and if not, it inserts the parameter as the new value for this key and returns
a mutable reference to the new value. This technique is much cleaner than writing the logic ourselves and,
in addition, plays more nicely with the borrow checker.

Running it will print `{"Yellow": 50, "Blue": 10}`. The first call to `entry` will insert the key for the Yellow
team with the value `50` because the Yellow team doesn't have a value already. The second call to `entry` will
not change the hash map becaues the Blue team already has the value of `10`.

<br>

*Updating a value based on the old value*

<br>

Another common use case for hashmaps is to look up a key's value and then update it based on the old value.
For instance, the code bellow shows code that counts how many time each word appears in some text. We use
a hash map with the words as keys and increment the value to keep track of how many times we've seen that word.
If it is the first time, we'll first insert the value `0` :

```rust
use std::collections::HashMap;

let text = "hello world wonderful world";

let mut map = HashMap::new();

for word in text.split_whitespace() {
    let count = map.entry(word).or_insert(0);
    *count += 1;
}

println!("{map:?}");
```

This code will print `{"world": 2, "hello": 1, "wonderful": 1}`. We might see the same key-value pairs printed
in a different order: recall that iterating over a hashmap happens in an arbitrary order.

The `split_withspace` method retunrs an iterator over subslices, separated by whitespace, of the value in `text`.
The `or_insert` method returns a mutable reference (`&mut V`) to the value for the specified key. Here,
we store the mutable reference in the `count` variable, so in order to assign to the value, we must first
dereference `count` using the asterisk `*`. The mutable reference goes out of scope at the end of the `for` loop,
so all of these changes are safe and allowed bby the borrowing rules.
