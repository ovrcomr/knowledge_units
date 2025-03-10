**Providing new names**

<br>

A solution to the problem of bringing two types with the same name into the same scope with `use`, after the path,
we can specify `as` and a new local name, or *alias* for the type :

```rust
use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {
    // --snip--
}

fn function2() -> IoResult<()> {
    // --snip--
}
```

This avoid naming conflicts while importing multiple things with the same name in the same scope.
