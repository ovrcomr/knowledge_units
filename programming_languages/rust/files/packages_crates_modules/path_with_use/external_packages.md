**External packages**

<br>

There is an external package called `rand` to get random numbers. To use `rand` in a project, we add
this line to *Cargo.toml* :

<br>

```toml
rand = "0.8.5"
```

<br>

Adding `rand` as a dependency in *Cargo.toml* tells Cargo to download the `rand` package and any dependencies
from *crates.io* and make `rand` available to the project.

Then, to bring `rand` definition into scope of our package, we added a `use` line starting with the name of the
crate, `rand`, and listed the items we wanted to bring into scope. For example, bringing the `Rng` trait into
scope and calling the `rand::thread_rng` function :

<br>

```rust
use rand::Rng;

fn main() {
    let secret_number = rand::thread_rng().gen_range(1..=100);
}
```

Members of the Rust community have made many packages available at *crates.io*, and pulling any of them into
a package involves these same steps: listing them in the package's *Cargo.toml* file and using `use` to bring
items from their crates into scope.

Not that the standard library `std` is also a crate that is external to our package. Because the standard library
is shipped with the Rust language, we do not need to change *Cargo.toml* to include `std`. But we need to
refer to it with `use` to bring items from there into our package's scope.

<br>

```rust
use std::collections::HashMap;
```

<br>

This is n absolute path starting from `std`, the name of the standard library crate.
