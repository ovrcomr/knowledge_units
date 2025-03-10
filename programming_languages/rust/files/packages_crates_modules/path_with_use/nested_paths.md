**Nested paths**

<br>

When using multiple items defined in the same crate or same module, listing each item on a separate line
is not practical. Instead, we can use nested paths to bring the same items into scope in one line :

<br>

```rust
// Without nesting
use std::cmp::Ordering;
use std::io;

// With nesting
use std::{cmp::Ordering, io};
```

<br>

We can use a nested path at any level in a path, which is useful when combining two `use` statements that share a
subpath :

<br>

```rust
// Without nesting
use std::io;
use std::io::Write;

// With nesting
use std::io::{self, Write};
```
