**Module separation**

<br>

When modules get large, we might want to move their definition to a separate file to make the code easier to navigate.

From the expample where there is multiple restaurant modules. Well will extract modules into files instead
of having all the modules defined in the crate root file. In this case, the crate root file is `src/lib.rs`, but
this procedure also works with binary crates whose crate root file is `src/main.rs`

First, the extraction of `front_of_house` module to its own file. The code inside the curly brackets is removed
for the `front_of_house` module, leaving only the `mod front_of_house;` declaration, so that `src/lib.rs` contains
the code :

<br>

```rust
mod front_of_house;

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

<br>

Then, inside the newly created `src/front_of_house.rs` :

<br>

```rust
pub mod hosting {
    pub fn add_to_waitlist() {}
}
```

<br>

Note that we only need to load a file using a `mod` declaration *once* in our module tree. Once the compiler
knows the file is part of the project (and knows where in the module tree the code resides because of where
we have put the `mod` statement), other files in the project should refer to the loaded file's code using a path
to where it was declared. In other words, `mod` *is not* an "include" operation that we may have seen in other
programming languages.

Next, we will extract the `hosting` module to its own file. The process is slightly different because `hosting`
is a child module of `front_of_house`, not of the root module. We will place the file for `hosting` in a new
directory that will be named for its ancestors in the module tree, in this case `src/front_of_house`

To start moving `hosting`, we change `stc/front_of_house.rs` to contain only the declaration of the `hosting`
module :

<br>

```rust
// src/front_of_house.rs
pub mod hosting;
```

<br>

Then we create a `src/front_of_house/hosting.rs` :

<br>


```rust
// src/front_of_house/hosting.rs
pub fn add_to_waitlist() {}
```

<br>

If we instead put `hosting.rs` in the `src` directory, the compiled would expect the `hosting.rs` code to be in
a `hosting` module declared in the crate root, and not declared as a child of the `front_of_house` module.
The compiler's rules for which files to check for which modules' code mean the directory and files more closely
match the module tree.

<br>

---

<br>

**Alternate file paths**

<br>

Rust also supports an older style of file path. For a module named `front_of_house` declared in the crate root,
the compiler will look for the module's code in :

- `src/front_of_house.rs` (what has been covered)
- `src/front_of_house/mod.rs` (older style, still supported path)

For a module named `hosting` that is a submodule of `front_of_house`, the compiler will look for the module's
code in :

- `src/front_of_house/hosting.rs` (what had been covered)
- `src/front_of_house/hosting/mod.rs` (older style, still supported)

If using both styles for the same module, the compiler won't work properly. The main downside of the style
that uses files named `mod.rs` is that the project can end up with many files named `mod.rs`, which can
get confusing when having them open in the editor at the same time.
`
