**Paths**

<br>

A path can take two froms :

- *Absolute* : Full path starting from a crate root; for code from an external crate, the absolute path begins
  with the crate name, and for code from the current crate, it starts with the literal `crate`.
- *Relative* : Starts for the current module and uses `self , super`, or an identifier in the current module.

Both are followed by one or more identifiers separated by double colon (`::`).

E.g. calling `add_to_waitlist()` inside a new `eat_at_restaurant()` function :

```rust
mod front_of_house {
    pub mod hosting {
        fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    crate::front_of_house::hosting::add_to_waitlist(); // Absolute path
    // Because eat_at_restaurant is in the same crate as the function, `crate` can be used
    front_of_house::hosting::add_to_waitlist(); // Relative path
    // Because the module is at the same level of the module tree as eat_at_restaurant,
    // it is possible to start the path with front_of_house
}
```

Choosing between absolute and relative is based on the project, and depends on wether we'll more likely move items
definitions code separatly from or together with the code that uses the item. In some case, mooving definitions
can cause an absolute path to be invalid, but at the same time a relative could remains correct.

The module that contains the required element needs to be public in order to enable access to the element.
Every item (function, struct...) is private from its parent module by default. So if an item needs to be private,
placing it inside a module is a functional approach.

Items in a parent module cannot access private items inside child modules, but items in child modules
can access items in their ancestor modules, as long as those items are public. In short everything that is not
public is private, regardless of the module-tree level they are. (This is mentionned because it is not the case
for parent modules in some other languages, where parents have a granted acess to every children content)

Rust choose to have the module system function this way so that hiding inner implementation details is the default.
Thay way, we know which parts of the inner code we can change without breaking outer code. However, it does give
the option to expose inner parts of child modules code to outer ancestor modules by using `pub` to make an item
public.

<br>

---

<br>

**Path exportation with pub**

Even if the module is public, access to its item(s) are not granteed.
Each item that need to be accessed outside from the module has to be public with `pub`.
The `pub` keyword on a module only lets code in its anscestor modules refer to it, not access its inner code.

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {} // Here, without pub, the function couldn't be accessed from outside
    }
}

pub fn eat_at_restaurant() {
    crate::front_of_house::hosting::add_to_waitlist(); // Absolute
    front_of_house::hosting::add_to_waitlist(); // Relative
}
```

If a library crate is planned to be shared, the public API is the contact with users of the crate that
determines how they can interact with the code. There are many considerations around managing changes to
a public API to make it easier for people to depend on the crate. [to go further](https://rust-lang.github.io/api-guidelines/)

*Best practices for package with binary and library*

A package can contain both a `src/main.rs` binary crate root and `src/lib.rs` library crate root, and both
crates will have the package name by default. Packages with this pattern of containing both a lib and bin crate
will have just enough code in the binary to start an executable that calls code within the library crate.
This lets other projects benefits from most of the functionality that the package provides because the
library crate's code can be shared.

The module tree should be defined in `src/lib.rs`. Then, any public items can be used in the binary crate
by starting paths with the name of the package. The binary crate becomes a user of the library crate just like
a completly external crate would use the library crate : it can only use the public API. This helps desinging
a good API; not only being the author of it, but also a user.
