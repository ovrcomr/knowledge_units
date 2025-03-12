**HashMap owernship**

<br>

For types that implement the `Copy` trait, like `i32`, the value are copied into the hashmap.
For owned values like `String`, the values will be moved and the hashmap will be the owner of those values :

<br>

```rust
use std::collections::HashMap;

let field_name = String::from("Favorite color");
let field_value = String::from("Blue");

let mut map = HashMap::new();
map.insert(field_name, field_value);
// field_name and field_value are invalid at this point, try using them and
// see what compiler error you get!
```

<br>

We are not able to use the variables `field_name` and `field_value` after they have been moved into the hashmap
with the call to insert.

If we insert references to values into the hashmap, the values won't be moved into the hashmap. The values that
the references point to must be valid for at least as long as the hash map is valid.
