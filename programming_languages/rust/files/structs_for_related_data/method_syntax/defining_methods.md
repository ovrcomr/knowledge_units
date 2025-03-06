*Methods* are similar to functions: we declare them with the `fn` keyword and a name,
they can have parameters and return a value, and they contain some code that is run when the
method is called from somewhere else. Unlike functions, methods are definded within the context
of a struct (or an enum or a trait object) and their first parameter is always `self`, which
represent te instance of the struct the method is being called on.

---

**Defining methods**

Let's change the `area` function that has a `Rectangle` instance as a parameter and instead
make an `area` method defined on the `Rectangle` struct, as shown here :

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

To define a function within `Rectangle`, we use an `impl` block. This associates all methods
inside it with `Rectangle`. The `area` function is moved inside, replacing `rectangle: &Rectangle`
with `&self`, which is shorthand for `self: &Self`. The `Self` type refers to the `struct` within
the `impl` block.

In `main`, instead of calling `area(rect1)`, we use method syntax: `rect1.area()`. This improves
readability and avoids repeating the type.

Methods can take self in three ways:

- `&self`: Borrows immutably (common for read-only operations).
- `&mut self`: Borrows mutably (used when modifying the instance).
- `self`: Takes ownership (rare, usually for transformations).

Using methods improves code organization, grouping all related behaviors within an `impl` block,
making it clearer and easier to use.

Unlike some languages, Rust separate **data** and **behavior**, this is why fields and methods are
not defined in the same block of code.

Note that we can choose to give a method the same name as one of the struct’s fields.
For example, we can define a method on Rectangle that is also named width:

```rust
impl Rectangle {
    fn width(&self) -> bool {
        self.width > 0
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    if rect1.width() {
        println!("The rectangle has a nonzero width; it is {}", rect1.width);
    }
}
```

Here, we are choosing the make the `width` method and return `true` if the value in the
instance's `width` field is greater than `0` and `false` if the value is `0`: we can
use a field within a method of the same name for any purpose. In main, when we follow
`rect1.width` with parentheses, Rust knows we mean the method `width`.
When we don’t use parentheses, Rust knows we mean the field `width`.

Often, but not always, when we give a method the same name as a field we want it to only
return the value in the field and do nothing else. Methods like this are called getters,
and Rust does not implement them automatically for struct fields as some other languages
do. Getters are useful because you can make the field private but the method public, and
thus enable read-only access to that field as part of the type’s public API.

---

In C and C++, two different operators are used for calling methods: you use . if you’re calling a method on the object directly and `->`
if you’re calling the method on a pointer to the object and need to dereference the pointer first. In other words, if object is a pointer,
object->something() is similar to (*object).something().

Rust doesn’t have an equivalent to the -> operator; instead, Rust has a feature called automatic referencing and dereferencing.
Calling methods is one of the few places in Rust with this behavior.

Here’s how it works: when you call a method with `object.something()`, Rust automatically adds in
&, `&mut`, or `*` so object matches the signature of the method. In other words, the following are
the same:

```rust
p1.distance(&p2);
(&p1).distance(&p2);
```

The first one looks much cleaner. This automatic referencing behavior works because methods
have a clear receiver—the type of `self`. Given the receiver and name of a method, Rust can
figure out definitively whether the method is reading `(&self)`, mutating `(&mut self)`, or
consuming `(self)`. The fact that Rust makes borrowing implicit for method receivers is a
big part of making ownership ergonomic in practice.
