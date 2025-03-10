**Bring path into scope**

<br>

`use` allows to create a shortcut to a path, and then use the shorter name everywhere else in the scope.
Here, we bring `crate::front_of_house::hosting` module into scope of the `eat_at_restaurant` function so we
only have to specify `hosting::add_to_waitlist` to call the `add_to_waitlist` function in `eat_at_restaurant` :

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

Adding `use` to a path in a scope is similar to creating a symoblic link in the filesystem.
By adding `use crate::front_of_house::hosting` in the crate root, `hosting` is now valid name in that scope.
Paths brought into scope with `use` also check privacy, like any other paths.

Note that `use` only creates the shortcut for the particular scope in which the `use` occurs :

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting; // Bring hosting to the outer scope

mod customer { // The path is no longer available in the inner scope of this module, causing an error
    pub fn eat_at_restaurant() {
        hosting::add_to_waitlist();
    }
}
```

To fix this case, the `use` has to be moved within the `customer` module too, or using the `super::hosting`
within the child `customer` module.

<br>

---

<br>

**Idiomatic use paths**

<br>

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting; // Idiomatic way to bring a function into scope
// Other case : use crate::front_of_house::hosting::add_to_waitlist; that only brings the specified function.

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    // The other call would simply be : add_to_waitlist();
}
```

The used way is the idiomatic way to bring a function into scope with `use`. Brining the function's parent module
into scope with `use` means we have to specify the parent module when calling the function. Specifying the parent
module when calling the function makes it clear that the function is not locally defined while still minimizing
repetition of the full path.

On the other hand, when bringing in structs, enums, and other items with `use`, it is idiomatic to specify the
full path :

```rust
use std::collections::HashMap;

fn main() {
    let mut map = HashMap::new();
    map.insert(1, 2);
}
```

There is no strong reason behind this idiom : it is just the convention that has emerged, and folks have gotten
used to reading and writing Rust code this way.

The exception to this idiom is if we are bringing two items with the same name into scope with `use`,
because Rust does not allow that :

```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {
    // --snip--
}

fn function2() -> io::Result<()> {
    // --snip--
}
```

Using the parent module distinguishes the two `Result` types. If instead we specified `use std::fmt::Result` and
`use std::io::Result`, we do have to `Result` types in the same scope, and Rust would not know which one we meant
when we used `Result`
