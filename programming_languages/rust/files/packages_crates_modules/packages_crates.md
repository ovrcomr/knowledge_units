**Crates**

<br>

A *crate* is the smallest amount of code that the compiler consider at a time.
*Crates* can contains modules, and the modules can be defined in other files that get compiled with the crate.

It can be either :

- *Binary crate* : Programs that can be compiled to an executable that can be used. Each must have a `main` function.
- *Library crate* : Don't have `main` function, and do not get compiled to an executable.
  They define functionality intended to be shared with mutliple projects.

Most of the time, when the term *crate* is used, it refers to a *library crate*.

The *crate root* is a source file that the compiler starts from and make up the root module of the crate.

---

**Packages**

A *package* is a bundle of one or more crates that provides a set of functionalities.
It contains a *Cargo.toml* file that describes how to build those crates.
Cargo is a package that contains the binary crate for the CLT (command line tool), used to build the code.
The Cargo package also contains a library crate that the binary crate depends on.
(Other projects can depends on the Cargo library)

A *package* can contain as many binary crate as wished, and at most one library crate.
It must contain at least one crate (binary or library)

<br>

---

<br>

**Package creation**

```bash
$ cargo new my-project
     Created binary (application) `my-project` package
$ ls my-project
Cargo.toml
src
$ ls my-project/src
main.rs
```

The `my-project` package contains :
- A `Cargo.toml` file
- A `my-project/src` folder that contains (by default) `main.rs`

Cargo follows a convention `src/main.rs` is the crate root of a binary crate with the same name as the package.
The crate root is where the program compilation begins, and the generate executable will have the same name as the package.

Likewise, if there is a `src/lib.rs`,  Cargo knows that the package contains a library crate with the same name as
the package, and `src/lib.rs` will be the crate root.

Cargo passes the crate root files to `rustc` to build the library or binary.

Here, we have a package that only contains src/main.rs, meaning it only contains a binary crate named my-project.
If a package contains src/main.rs and src/lib.rs, it has two crates: a binary and a library, both with the same name
as the package.
A package can have multiple binary crates by placing files in the src/bin directory: each file will
be a separate binary crate.
