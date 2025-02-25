Let's practice using methods by implementing a second method on the `Rectangle` struct.
This time we want an instance of `Rectangle` to take another instance of `Rectangle` and return
`true` if the second `Rectangle` can fit complitely within `self` (the first `Rectangle`); otherwise,
it should return `false`.

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```

When we run this code with the main function in Listing 5-14, we’ll get our desired output.
Methods can take multiple parameters that we add to the signature after the self parameter,
and those parameters work just like parameters in functions.
