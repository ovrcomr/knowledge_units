<br>

**Tuple type**

A *tuple* is a general way of grouping together a number of values with a variety of types into one compound type.
Tuples have fixed length : once declared, it cannot grow or shrink in size.

Tuples are created by writing a comma-separeted list, of values inside braces. Each position as a type, and types doesn't have to be the same :

```rust
fn main() {

    let tup: (i32, f64, u8) = (500, 6.4, 1);

}
```

The variable `tup` binds to the entire tuple because a tuple is considered a single compound element.
To get the individual values out of a tuple, it is possible to use the pattern matching to destructure a tuple value :

```rust
fn main() {

    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let (x, y, z) = tup;

    println!("The value of y is : {y}")

}
```

This program first create a tuple `tup`, and then use *destructuring* to assign to different (x, y and z) variable each values of the tuple.
x is assinged to `500`, y to `6.4` and `z` to `1`. It's also possible to access element using tuple index (start from 0) :

```rust
fn main() {

    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let five_hundred = tup.0;
    let six_dot_four = tup.1;
    let one = tup.2;

}
```

A tuple without any value has a special name : unit. This value and its corresponding type are both written () and represent en empty value or an empty
return type. Expressions implicitly return the unit value if they don't return any other value.

---

**Array type**

Array represent another way to collect multiple values. Unlike tuples, every element of an array must have the same type and have a fixed length.

```rust
fn main() {

    let a = [1, 2, 3, 4, 5];

}
```

Arrays are useful when the data need to be allocated on the stack rather than on the heap, or when a developer wants to ensure to have a fixed number of elements.
Vectors are similar to arrays, but they can grow or shrink. They are provided by the standard library. Arrays remains useful when having a pre-defined number of elements.
A usecase of array can be month representation.

To specify the type of an array :

```rust
let a: [i32, 5] = [1, 2, 3, 4, 5]; // [type, number_of_element]
```

It's also possible to initialize an array to contain the same value for each elements :

```rust
let a: [3; 10]; // [elements_value, number_of_element]
```

**Accessing element**

Elements can be accessed using index (start from 0):

```rust
fn main() {

    let a: [i32, 5] = ["First", "Second", "Third", "Fourth", "Fifth"];
    let first = a[2]; // Third

}
```

When trying to access an element in a list, Rust will verify if the provided index is greater that the array length.
If the index is greater or equal (last index is number_of_element - 1; array.len() - 1), the compiler will *panic* and exit the program.
