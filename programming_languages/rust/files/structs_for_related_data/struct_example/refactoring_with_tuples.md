To understand when we might want to use structs, there is a program that calculates the area of a rectangle.
We will start by using single variables, and then refactor the program until we are using structs instead.

```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(with: u32, height: u32) -> u32 {
    width * height
}
```

---

The code might be more readable using tuples :

```rust
fn main() {
    let rect1 = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect1)
    );
}

fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1
}
```

Tuples leads to a bit of structure, and we are now passing just one argument. In the other hand, tuples do not
name their elements, so we have to index into the parts of the tuple, making the calculation inside
`area()` less obvious.
