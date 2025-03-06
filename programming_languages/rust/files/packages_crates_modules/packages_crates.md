About *crates* :

- Is the smallest amount of code that the Rust compiler consider at a time.
- Can contain modules, and modules may be defined in other files that get compiled with the crate.
- Can come in two different forms
  - A binary crate : programs that can be compiled to an executable that can be runned.
  - A library crate : don't have a `main()`, and do not compile to an executable. They define functionality intended to be shared with
    mutliple projects.

When the word *crate* is used, it most of the time refers to a *library crate*, and use *crate* interchangeably with the general programming
concept of *library*.

The *crate root* is a source file that the Rust compiler starts from and makes up the root module of a *crate*.

---

About *packages* :

- Is a bundle of one or more *crates* that provides a set of functionality.
- Contains a *Cargo.toml* file that describes how to build those crates. Cargo is a package that contains the binary crate for the command-line tool and a library crate that the binary carte depends on.
- Can contain as many binary crates as needed, but at most only one library crate.
- Must contain at least one crate, wether that is a library or binary crate.

---

To create a package, run `cargo new project_name`. This generates a directory containing a `Cargo.toml file`, which defines the package.

*Cargo* follows a convention:
- `src/main.rs` is the crate root for a binary crate with the same name as the package.
- `src/lib.rs` is the crate root for a library crate.

Initially, a package with only `src/main.rs` contains a single binary crate. If `src/lib.rs` is added, the package includes both a binary and a library crate, both named same as the package.
To include multiple binary crates, place additional Rust files in `src/bin/`, each becoming a separate binary crate.
