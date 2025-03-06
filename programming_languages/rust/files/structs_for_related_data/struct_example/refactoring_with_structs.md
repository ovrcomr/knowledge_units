Here is the version of the code using structs :

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

Here we’ve defined a struct and named it `Rectangle`. Inside the curly brackets, we defined the
fields as width and height, both of which have type `u32`. Then, in main, we created a particular
instance of Rectangle that has a `width` of `30` and a `height` of `50`.

Our area function is now defined with one parameter, which we’ve named `rectangle`, whose type is
an immutable borrow of a struct `Rectangle` instance. We want to borrow the struct rather than
take ownership of it. This way, main retains its ownership and can continue using `rect1`,
which is the reason we use the `&` in the function signature and where we call the function.

The `area` function accesses the `width` and `height` fields of the `Rectangle` instance
(note that accessing fields of a borrowed struct instance does not move the field
values, which is why you often see borrows of structs). Our function signature for
area now says exactly what we mean: calculate the area of `Rectangle`, using its `width`
and `height` fields. This conveys that the `width` and `height` are related to each other,
and it gives descriptive names to the values rather than using the tuple index values
of `0` and `1`. This is a win for clarity.
