Relative paths can begin in the parent module, rather than the current module or the crate root, by using
`super` at the start of the path. This is like starting a filesystem path with the `..` syntax.
Using `super` allows to reference an item that we know is in the parent module, which can make rearranging the
module tree easier when the module is closely related to the parent but the parent might be moved elsewhere in
the module tree.

```rust
fn deliver_order() {}

mod back_of_house {
    fn fix_incorrect_order() {
        cook_order();
        super::deliver_order();
    }

    fn cook_order() {}
}
```

The `fix_incorrect_order` function is in the `back_of_house` module, so we can use `super` to go to the parent
module of the `back_of_house`, which in this case is `crate`, the root. From there, we can look for
`deliver_order` and find it.
