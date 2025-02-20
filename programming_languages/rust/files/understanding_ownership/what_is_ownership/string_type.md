Understanding Ownership with String
To explore Rust’s ownership rules, we need a more complex data type than the simple types covered in Chapter 3. Those basic types have a fixed size, making them easy to store on the stack. Since stack values are automatically removed when they go out of scope, they can be copied quickly and efficiently.

However, some data—especially when its size is unknown at compile time—must be stored on the heap. Rust needs to manage this memory properly, ensuring it’s cleaned up when no longer needed. The String type is a great example of how Rust handles heap-allocated data.

String Literals vs. String
We’ve already seen string literals—hardcoded string values embedded in our code. While convenient, string literals have two limitations:

They are immutable – You cannot modify them.
They must be known at compile time – You can’t use them for dynamic input, like storing user-provided text.
To handle dynamic text storage, Rust provides the String type, which is allocated on the heap and can grow or shrink as needed. You can create a String from a string literal like this:

```rust
let s = String::from("hello");
```

The `::` (double colon) operator is used to call the from function specifically from the String type. We’ll cover more on this syntax in Chapter 5 (Method Syntax) and Chapter 7 (Modules and Namespacing).

Mutability and Memory Differences
Unlike string literals, String values can be modified:

```rust
let mut s = String::from("hello");

s.push_str(", world!"); // Appends ", world!" to the existing String

println!("{s}"); // Prints: hello, world!
```

So, why is String mutable, but string literals are not? The answer lies in memory management:

String literals (&str) are stored in the stack as read-only memory. They are fixed in size and cannot change.
String is stored in the heap, allowing it to grow and be modified dynamically.
