[**Tuples**](https://doc.rust-lang.org/rust-by-example/primitives/tuples.html) can bring together mutliple values with a variety of types into one compound type.
Tuples have fixed length : once declared, it cannot grow or shrink in size.

Tuples are created by writing a comma-separeted list, of values inside braces.
Each position as a type, and types doesn't have to be the same.
`tup` binds to the entire tuple because a tuple is considered a single compound element :

```rust
// Definition

let tup: (i32, f64, u8) = (500, 6.4, 1);

// Accessing element
let tup_first_element = tup.0; // 500 // Acess by index
let (x, y, z) = tup // x = 500, y = 6.4, z = 1 // Access by destructuring

// Modifying element
let mut person: (&str, i32) = ("John", 38); // mutable tuple
person.0 = "Peter"; // person = ("Peter", 38)

```

A tuple without any value is the **unit** type. Written by `()`, it represents en empty value or an empty
return type. Expressions implicitly return the unit value if they don't return any other value.

<br>

---

<br>


[**Arrays**](https://doc.rust-lang.org/rust-by-example/primitives/array.html) represent another way to collect multiple values.
- All the values inside must have the same type (unlike tuples).
- The size is fixed at declaration (like tuple).

```rust
// Definition

let first_numbers = [1, 2, 3, 4, 5]; // simple definition
let first_numbers: [i32; 5] = [1, 2, 3, 4, 5]; // [stored type, number of element]
let ten_three: [3; 10]; // [value of each element, number of element]

// Accessing element

let second_array: [&str, 2] = ["Hello", "World", "Code"];
let last_element = second_array[2]; // Code

// Modifying element

let mut names: [&str; 2] = ["Hello", "World"]; // mutable array
names[0] = "Goodbye"; // names = ["Goodbye", "World"]
```

Arrays are useful when :
- The data need to be on the stack (rather heap stored)
- Ensuring a fixed number of elements.

[**Vectors**](https://doc.rust-lang.org/rust-by-example/std/vec.html) only differ from *arrays* because they can grow/shrink in size during execution.
