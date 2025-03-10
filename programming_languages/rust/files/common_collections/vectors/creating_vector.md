Vectors (`Vec<T>`) allows to store more than one value in a single data structure that pulls all the values
next to each other in memory. Vectors can only stores values of a same type. They are useful when having a list
of items, such as the lines of text in a file or the piece of items in a shopping cart.

<br>

---

<br>

**Vector creation**

<br>

To create a new empty vector, we call the `Vec::new` function :

<br>

```rust
let new_vector: Vec<i32> = Vec::new();
```

<br>

Note that when declaring a vector, the type that it will contain must be specifiyed. This is important, vectors
are implemented using generics. For now, know that the `Vec<T>` type provided by the standard library can hold any
type. When we create a vector to hold a specific type, we can specify the type within angle brackets.

More often, we will create a `Vec<T>` with initial values and Rust infer the desired value type, so wa rarely
need to do this type annotation. Rust conveniently provides the `vec!` marco, which will create a new vector that
holds the values we give it :

<br>

```rust
let new_vector = vec![1, 2, 3];
```

<br>

Because we have given initial `i32` values, Rust can infer that the type of `new_vector` is `Vec<i32>`, and the
type annotation is not necessary.
