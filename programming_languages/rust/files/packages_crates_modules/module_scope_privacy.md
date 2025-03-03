- **Start from the crate root** : When compiling a crate, the compiler first look in the crate root file for code to compile.

- **Declaring modules** : In the crate root file, new modules can be declared, as `mod module_name`, the compiler will look for the module's
  code in theses places :
  - Inline, within curly braces that replace the semicolon following `mod module_name`
  - In the file `src/module_name.rs`
  - In the file `src/module_name/mods.rs`

- **Declaring submodules** : In any file other than the crate root, submodules can be declared. For instance, `mod submodule_name` might be
declared in `src/module_name.rs`. The compiler will look for the submodule's code within the directory named for the parent module in these places :
  - Inline, directly within curly brackets that replace the semicolon following `mod module_name`
  - In the file `src/module_name/submodule_name.rs`
  - In the file `src/module_name/submodule_name/mod.rs`

- **Paths to code in modules** : Once a module is part of a crate, it can be refered to code in that module from anywhere else in that same crate,
  as long as the privacy rules allows, using the path to the code. For example : `crate::module_name::submodule_name::type_name`.

- **Private vs. public** : Code within a module is private from its parent modules by default. `pub mod` (instead of `mod`) makes a module
  public. `pub` can also be used for items within the module to make them public as `pub item_name` (inside `pub` module).

- **The `use` keyword** : Within a scope, the `use` keyword creates shortcuts to items to reduce repetition of long paths. In any scope that can refer to
  `crate::module_name::submodule_name::type_name` with `use crate::module_name::submodule_name::type_name`; and from then on it is only required to write `type_name`
  to make use of that type in the scope.

---

Here is a binary crate named `backyard` that illustrates these rules. That crate's directory, also named `backyard`, contains these files and directories :

```txt
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │    └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

The crate root file in this case is `src/main.rs`, and it contains :

```rust
use crate::garden::vegetable::Asparagus;

pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {plant:?}!")
}
```

The `pub mod garden;` line tells the compiler to include the code it finds in `src/garden.rs` which is :

```rust
pub mod vegetables;
```

Here, `pub mod vegetables;` means the code in `src/garden/vegetables.rs` is included too. That code is :

```rust
#[derive(Debug)]
pub struct Asparagus {}
```

---

**Grouping related code in modules**

Modules allows :
- Orgnaizing code within a crate for readability and reuse
- Control the *privacy* of items because code within a module is private by default. It can be choosed to make some of them public, for external usage.

Illustration : library crate of a restaurant.

```rust
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
}
```

We define a module with the `mod` keyword followed by the name of the module.
We can place other modules inside another, and can hold definition of other items such as structs, enums, constants, traits...
Modules allows to group related definitions together.

```txt
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```

This three shows how some of the modules nest inside other modules (parent/child) or in the case multiple modules are inside another they are simblings.
The entire tree is rooted under the implicit module named `crate`.
