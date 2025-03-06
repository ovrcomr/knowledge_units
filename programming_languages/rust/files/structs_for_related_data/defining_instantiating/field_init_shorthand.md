A struct, or structure, is a custom data type that lets package together and name multiple
related values that make up a meaningful group. If you’re familiar with an object-oriented
language, a struct is like an object’s data attributes. In this chapter, we’ll compare and
contrast tuples with structs to build on what you already know and demonstrate when structs
are a better way to group data.

---

*Structs* are similar to tuples, in that both hold mutliple related values. Like tuples,
the pieces of a struct can be different types. Unlike with tuples, in a struct, each piece
of data can be named in a clear and meaningful way. Adding these names means that structs are
more flexible than tuples: you don't have to rely on the order of the data to specify or access
the values of an instance.

- To define a struct, we use the `struct` keyword
- A struct name should describe the significance of stored data

```rust
struct User {
    is_active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```

After creating a struct, that can be seen as a template, it is possible to create
instances of that struct, by specifing concrete values for each of the fields.
An instance is created first by stating the name of the struct that it will use, and
then add *key: value* pairs, where *key* is the name of the field, and *value* is the data
stored along to it. We don't have to specify the fields in the same order in which we
declared them in the struct.

```rust
fn main() {

    struct User {
        active: bool,
        username: String,
        email: String,
        sign_in_count: u64,
    }

    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
}
```

To get a specific value from an instance, we use dot notation. For example, to access this user's
email address, we use user1.email. If the instance is mutable, we can change a value by using the
dot notation and assigin into a particular field :

```rust
fn main() {

    struct User {
        active: bool,
        username: String,
        email: String,
        sign_in_count: u64,
    }

    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```

The entire instance must be mutable; Rust doesn't allow us to mark only certain fields as mutable.
As with any expression, we can *constrcut* a new instance of a struct as the last expression in the
function body to implicitly return the new instance :

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        email: email,
        sign_in_count: 1,
    }
}
```

It make sense to name the function parameter with the same name as the struct fields, but having
to repeat the `email` and `username` field names and variables is a bit tedious. If the struct
had more fields, repeating each name would get even more annoying.

---

**Using the field init shorthand**

Because the parameter names and the struct fields name are exactly the same,
we can use the *field init shorthand* syntax to rewrite `build_user` so it behaves exactly
the same but does not have the repetition of `username` and `email` :

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```

Here, we are creating a new instance of the `User` struct, which has field named `email`.
We want to set the `email` field's value to the value in the `email` parameter of the
`build_user` function. Because the `email` field and the `email` parameter have the same
name, we only need to write `email` rather than `email: email`.
