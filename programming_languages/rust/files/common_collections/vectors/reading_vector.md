**Reading elements from vectors**

<br>

There are two ways to reference a value stored in a vector :
- Indexing
- Using the `get()` method

<br>

```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
println!("The third element is {third}");

let third: Option<&i32> = v.get(2);
match third {
    Some(third) => println!("The third element is {third}"),
    None => println!("There is no third element."),
}
```

<br>

Vectors are indexed from `0` meaning that the first element's index is `0`, the second is `1`...
Using `&` and `[]` gives us a reference to the element at the index value. When we use the `get` method
with the index passed as an argument, we get an `Option<&T>` that we can use with `match`.

Rust provides these two ways to reference an element so you can choose how the program behaves when you try
to use an index value outside the range of existing elements. Using he `get()` method is more sustainable
because it will handle the case where we try accessing a non-existing element (index) without causing
the compiler to panic. If the element at the requested index does not exist, the method will return `None`.

<br>

```rust
let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100];
let does_not_exist = v.get(100);

```

<br>

This is illustrated by this snippet of code.

In the case of using `get()`, when the program has a valid reference, the borrow checker enforces the ownership and
borrowing rules to ensure this reference and any other references to the contents of the vector remain valid.
Recall the rule that states it is not possible to have mutable and immutable references in the same scope.
That rule applies down bellow, where we hold an immutable reference to the first element in a vector and try to
add an element to the end. This program won't work if we also try to rfer to that element later in the function :

<br>

```rust
let mut v = vec![1, 2, 3, 4, 5];
let first = &v[0];
v.push(6);
println!("The first element is {first}");
```

<br>

This will produce an error because of the way vectors work : because vectors put the valus next to each other in
memory, adding a new element onto the end of the vector might require allocating new memory and copying the old
elements to the new space, if there is not enoug room to put all the elements next to each other where the vector
is currently stored. In that case, the reference to the first element would be pointing to deallocated memory.
The borrowing rules prevent programs from ending up in that situation.

[Deep understanding of vectors documentation](https://doc.rust-lang.org/nomicon/vec/vec.html)
