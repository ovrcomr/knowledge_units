According to the [previous step](./creating_project_directory.md), a directory
has been created to include the actual code.

Create a new source file and name it `main.rs`.
*Rust* file ends with the `.rs` file extension.

The conviention is, when the file name is multiple words, that they
are spearated using underscores `_` (*e.g. hello_wolrd.rs*)

Open `main.rs` and write :

```rust
fn main() {
    println!("Hello, world!");
}
```

Save it and compile it using the `rustc` compiler in the terminal :

```bash
$ rustc -o output_file_name main.rs
```

The following command compile the `main.rs` file, and create an output file
named `output_file_name`. But the output file it can be called whatever the user want in
order to be intuitive.

```bash
$ ./output_file_name
```

It will run the compiled program and print `Hello, world!`
