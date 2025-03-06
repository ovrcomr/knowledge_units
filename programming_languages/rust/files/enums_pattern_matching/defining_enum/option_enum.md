This section explores a case study of `Option`, which is another enum defined by the standard library. The
`Option` type encodes the very commom scenario in which a value could be something or it could be nothing.

For example, if we request the first item in a non-empty list, we would get a value. If we request the first
item in an empty list, you would get nothing. Expressing this concept in terms of the type system means the
compiler can check wether we have handled all the cases we should be handling; this functionality can prevent
bugs that are extremely common in other programming languages.

Programming language design is often thought of in terms of which features you include, but the features you
exclude are important too. Rust does not have the full feature that many other languages have. *Null* is a
value that means that there is no value there. In languages with *null*, variables can always be in one of
those two states : null or not-null.

The problem with null values is that if we try to use a null value as a not-null value, we will get an error of
some kind. Because this null or not-null property is pervasive, it is extremely easy to make this kind of error.
However, the concept that null is trying to express is still a useful one: a null is a value that is currently
invalid or absent for some reason.

The problem is not really with the concept but with the particular implementation. As such, Rust does not have
nulls, but it does have an enum that con encode the concept of a value being present or absent. This enum is
`Option<T>`, and it is defined by the *std lib* as follows :

```rust
enum Option<T> {
    None,
    Some(T),
}
```

The `Option<T>` enum is so useful that it is even included in the prelude; we do not need to bring it into scope
explicilty. Its variants are aslo included in the prelude: we can use `Some` and `None` directly without the
`Option::` prefix. The `Option<T>` enum is still just a regular enum, and `Some(T)` and `None` are still
variants of type `Option<T>`.

The `<T>` syntax is a feature of Rust we have not talked about yet. It is a generic type parameter. For now,
all we need to know is that `<T>` means that the `Some` variant of the `Option` enum can hold any type,
and that each concrete type that gets used in place of `T` makes the overall `Option<T>` type a different type.

---

```rust
let some_number = Some(5);
let some_char = Some('e');
let absent_number = Option<i32> = None;
```

The type of `some_number` is `Option<i32>`, the type of `some_char` is `Option<char>`, which isa different type.
Rust can infer these types because we have specified a value inside the `Some` variant. For `absent_number`, Rust
requires us to annotate the overall `Option` type: the compiler cannot infer the type that the corresponding `Some`
variant will hold by looking only at a `None` value. Here, we tell Rust that we mean for `absent_number` to be
of type `Option<i32>`.

When we have a `Some` value, we know that a value is present and the value is held within the `Some`. When we
have a `None` value, in some sense it means the same thing as null: we do not have a valid value. So why is having
`Option<T>` any better than having null ?

In short, because `Option<T>` and `T` (where `T` can be any type) are different types, the compiler won't let us
use an `Option<T>` value as if it were definitly a valid value. For example, this code won't compile, because
it is trying to add an `i8` to an `Option<i8>` :

```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);
let sum = x + y;
```

```bash
$ cargo run
   Compiling enums v0.1.0 (file:///projects/enums)
error[E0277]: cannot add `Option<i8>` to `i8`
 --> src/main.rs:5:17
  |
5 |     let sum = x + y;
  |                 ^ no implementation for `i8 + Option<i8>`
  |
  = help: the trait `Add<Option<i8>>` is not implemented for `i8`
  = help: the following other types implement trait `Add<Rhs>`:
            `&'a i8` implements `Add<i8>`
            `&i8` implements `Add<&i8>`
            `i8` implements `Add<&i8>`
            `i8` implements `Add`

For more information about this error, try `rustc --explain E0277`.
error: could not compile `enums` (bin "enums") due to 1 previous error
```

This error message means that Rust does not understand how to add an `i8` with an `Option<i8>`, because they are
different types. When we have a value of a type like `ì8` in Rust, the compiler will ensure that we always have
a valid value. We can proceed confidently without having to check for null before using that value. Only when
we have an `Option<i8>` (or whatever type of value we’re working with) do we have to worry about possibly
not having a value, and the compiler will make sure we handle that case before using the value.

In other words, we have to convert an `Option<T>` to a `T` before we can perform opertation with it.
Generally, the helps catch one of the most common issues with null: assuming that something is not null
when it actually is.

Eliminating the risk of incorrectly assuming a not-null value helps we to be more confident in our code.
In order to have a value that can possibly be null, you must explicitly opt in by making the type of that
value `Option<T>`. Then, when we use that value, we are required to explicitly handle the case when the value
is null. Everywhere that a value has a type that isn’t an `Option<T>`, we can safely assume that the value
isn’t null. This was a deliberate design decision for Rust to limit null’s pervasiveness and increase the
safety of Rust code.

So how do we get the `T` value out of a Some variant when we have a value of type Option<T> so that we can
use that value? The `Option<T>` enum has a large number of methods that are useful in a variety of situations;
we can check them out in its documentation. Becoming familiar with the methods on `Option<T>` will be extremely
useful.

In general, in order to use an `Option<T>` value, we want to have code that will handle each variant. We want
some code that will run only when we have a `Some(T)` value, and this code is allowed to use the inner T. We
want some other code to run only if we have a None value, and that code doesn’t have a `T` value available.
The match expression is a control flow construct that does just this when used with enums: it will run different
code depending on which variant of the enum it has, and that code can use the data inside the matching value.
