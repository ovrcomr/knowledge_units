**Module cheat sheet**

<br>

- *Start from the crate root* :  When compiling a crate, the compiler first look into the crate 'root file'.
  (If there is `main.rs`, with or without a `lib.rs`, it will produce a binary crate, if only `lib.rs`, library crate).

- *Declaring modules* : In the crate root file, it is possible to declare new modules, e.g. a *garden* module
  using `mod garden`. The compiler will look for the module's code in these places :
  - Inline : within curly braces that replaces the semicolon following the `mod garden`.
    ```rust
    mod garden {
          // Content of the garden module
    }
    ```
  - In the file `src/garden.rs`
  - In the file `src/garden/mod.rs`

- *Declaring submodules* : In any file other than the crate root, subm-odules can be declared, e.g. `mod vegetables`.
  The compiler will look for the sub-module's code within the directory named for the parent module in these places :
  - Inline, within curly brackets that replace the semicolon following `mod garden`
    ```rust
    mod garden {
        // Content of the garden module
        mod vegetable {
            // Content of the garden sub-module (vegetable module)
        }
    }
    ```
  - In the file `src/garden.rs`
  - In the file `src/garden/mod.rs`

- *Path to code in modules* : Once a module is part of a crate, it can be refered to code in that module from anywhere
  else in the same crate, as long as the privacy rules allow, using the path to the code, e.g. `Asparagus` type in the garden
  would be found at `crate::garden::vegetables::Asparagus`.

- *Private vs. public* : Code within a module is private from its parent modules by default. It is possible to make it
  public using `pub mod` (instead of `mod`). To make items within a public mode as well, `pub` can be used before the item's declaration :
  ```rust
  pub mod public_module {
      pub public_function() {
          // Content of the function
      }
  }
  ```

- *The `use` keyword* : Within a scope, `use` keyword creates shortcuts to items to reduce repetition of long paths.
  In any scope that can refer to `crate::garden::vegetable::Asparagus`, it is possible to create a shortcut with
  `use crate::garden::vegetable::Asparagus;`, and from then, `Asparagus` can be called without specifying the path anymore
  in the file the shortcut has been written in.

Here is the illustration of those rules :

```txt
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

The crate root in that case is `src/main.rs` and contains :

```rust
use crate::garden::vegetables::Asparagus;

pub mod garden; // Tells the compiler to include the code from `src/garden.rs`

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {plant:?}!");
}
```

```rust
// src/garden.rs
pub mod vegetables;
```

This means that the code in `src/garden/vegetables.rs` is included too. That code is :

```rust
#[derive(Debug)]
pub struct Asparagus {}
```

<br>

---

<br>

**Grouping related code in modules**

*Modules* allows organizing code within a crate for readability and easy reuse.
By default, everything inside of a *module* is private, it allows selecting what should be public or not, in a
explicit way, allowing external code to use what is public.

There is an illustration by the usecase of a restaurant :

Let's consider that in this industry, some parts are part of *the front of house*, where customers are, and the other are part of
*the back of house*, where everything is prepared.

To structure our crate in this way, functions can be organized in nested modules :

```bash
cargo new restaurant --lib
```

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

The module is defined with `mod` followed by the name of it. Inside it can be placed other modules, as in the case
of `hosting` and `serving`. Modules can also hold definitions for other items, such as structs, enums, traits,
functions...

By using modules, it enables grouping related defintions together and name why they are related.
It helps to add meaning and organization in a program, making updates and fixes easier to operate.

`src/main.rs` and `src/lib.rs` are the crate roots. The reason for their name is that the contents of either
of theses two files from a module named `crate` at the root of the crate's module structure, known as the *module
tree*

```bash
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

It shows how some of the modules nest inside other modules. It also shows that some modules are *simblings*,
meaning they are in the same module. There is also a *parent/child* like comparaison between modules.
The entire module tree is rooted under the implicit module named crate.
