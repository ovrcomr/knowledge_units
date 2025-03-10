**Global operator**

<br>

If we want to bring *all* public items defined in a path into scope, we can specify that path followed by `*` :

<br>

```rust
use std::collections::*;
```

<br>

This `use` statement brings all public items defined in the `std::collections` into the current scope.
Glob can make it harder to tell what names are in scope and where a name used was defined.

The glob operator is often used when testing to bring everything under test into the `tests` module.
It is also sometimes used as part of the prelude pattern.
