Cargo is Rust's build systym and package mananger.
It handles tasks such as building code, downloading libraries the code depends on,
and building those libraries. (Libraries are code dependencies).

For a basic code as :

```rust
fn main() {
    println!("Hello, world!");
}
```

There is no dependencies, Cargo is not required. But for bigger projects, cargo will
most likely be required to manage libraries, and creating from the start a projet
using Cargo will simplify the whole process.

---

To check Cargo's version :

```bash
$ cargo --version
```

---

To create a project with Cargo :

```bash
cargo new hello_cargo
cd ./hello_cargo
```

- `cargo new` will create a new project (directory) called 'hello_cargo'.
- `cd`is for going in the newly created project.

Cargo generates two files and one directory to start :

- `Cargo.toml` file
- `src` directory containing `main.rs` file

It also initialize the project with Git as a repository along with a `.gitignore`.
*Note : Git files won't be generated if runned inside an already existing git repo*

---

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "yyyy"

[dependencies]
```

- `[package]` is a section heading that indicates that the following statements are configuring a package.
- The next three lines set the configuration informations Cargo needs to compile the program.
- `[dependencies]` is the start of another section to list every of the project dependencies.

In Rust, packages of code are referred as *crates*.
Cargo expects sources (code) files to live inside the `src` directory.
The top-level project is for README, License, .gitignore and so on.
