From the cargo project directory, build the project with the following command :

```bash
$ cargo build
```

This command creates a executable (compiled) file in `target/debug/hello_cargo`
rather than in the current directory. Because the default build is a debug build,
Cargo puts the binary in a directory named `debug`.

To run the executable file after building the cargo project once :

```bash
$ ./target/debug/hello_cargo # project_name
```

Running `cargo build` for the first time causes Cargo to create a new file called `Cargo.lock`.
This file keeps track of exact versions of dependencies in the project.
This file will never require manual changes at some point, Cargo is in charge of it.

---

It's also possible to compiled and execute in a single command :

```bash
$ cargo run
```

This is more convenient than having to remember to run `cargo build` and then execute
with the command with the path up to binary.

---

The check the validity of the program, it's possible to use :

```bash
$ cargo check
```

This will check if the program can compile without erros, without creating a executable file.
This is particularly useful and faster when only checking if the program is bug free, it
will not take resources to write the executable file, making the checking process quicker.
