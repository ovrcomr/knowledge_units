**Updating vectors**

<br>

Here is the initial `new_vector` vector storing integers from 1 to 3 :

```rust
let mut new_vector = vec![1, 2, 3];
```

We can add elements to it using the `push` method, that takes as argument the value we want to insert :

```rust
new_vector.push(4); // new_vector = [1, 2, 3, 4]
```

It is possible to remove the last element of a vector using the `pop` method :

```rust
new_vector.pop() // new_vector is back to : [1, 2, 3]
```
