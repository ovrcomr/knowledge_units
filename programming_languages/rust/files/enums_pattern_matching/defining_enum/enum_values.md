Where structs give us a way of grouping together related fields and data, enums give us a way of saying
a value is one of a possible set of values. For example, we may want to say that `Rectangle` is one of a set
of possible shapes that also includes `Circle` and `Triangle`. To do this, Rust allows us the encode these
possibilites as an enum.

Let's look at a situation we might want to express in code and see why enums are useful and more appropriate
than structs in this case. Say we need to work with IP addresses. Currently, two major standars are used for
IP addresses: version four and version six. Because these are the only possibilities for an IP address that our
program will come across, we can *enumerate* all possible variants, which is where enumeration gets its name.

Any IP address can be either a version four or six, but not both at the same time. That property of IP address
makes the enum data structure appropriate because an enum value can only be one of its variants. Both version four
and six addresses are still fundamentally IP addresses, so they should be treated as the same type when the
code is handling situations that apply to any kind of IP address.

We can express this concept in code by defining an `IpAddrKind` enumeration and listing the possible kinds an
IP address can be, `V4` and `v6`. These are the variants of the enum :

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

`IpAddrKind` is now a custom data type that we can use elsewhere in our code.

---

**Enum values**

We can create instances of each of the two variants of `IpAddrKind` :

```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

Note that the variants of the enum are namespaced under its identifier, and we user a double colon `::` to
separate the two. This is useful because new both values `IpAddrKind::V4` and `IpAddrKind::V6` are of the same
type: `IpAddrKind`. We can then, for instance, define a function that takes any `IpAddrKind` :

```rust
fn route(ip_kind: IpAddrKind) {}
```

And we can call this function with either variant :

```rust
route(IpAddrKind::V4);
route(IpAddrKind::V4);
```

Using enums has even more advantages, Thinking more about our IP address type, at the moment we don't have a way
to store the actual IP address *data*; we only know what *kind* it is.

```rust
enum IpAddr {
        V4(String),
        V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
```

This is more concise than creating a struct and instanciate each type.
We attach data to each variant of the enum directly, so there is no feed for an extra struct. Here, it is also
easier to see another detail of how enums work: the name of each enum variant that we define also becomes a
function that constructs an instance of the enum. That is, `IpAddr::V4()` is a function call that takes a
`String` as an argument and returns an instance of the `IpAddr` type. We automatically get this constructor
function defined as a result of defining the enum.

There is another advantage of using an enum rather than a struct: each variant can have different types and amounts
of associated adta. Version four IP addresses will always have four numeric components that will have values
between 0 and 255. If we wanted to store `V4` addresses as four `u8` alues but still express `v6` addresses as
one `String` value, we would not be able to with a struct. Enums handle this case with ease :

```rust
enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1"));
```

We have shown several different ways to define data structures to store version four and version six IP addresses.
However, as it turns out, wanting to store IP adresses and encode which kind they are is so common that the
*standard library* has a definition we can use. Let's look at how the standard library defines `IpAddr` : it has
the exact enum and variants that we have defined and used, but it embeds the address data inside the variants
in the form of two different structs, which are defined differently for each variant.

```rust
struct Ipv4Addr {
    // --snip--
}

struct Ipv6Addr {
    // --snip--
}

enum IpAddr {
    V4(Ipv4Addr),
    V6(Ipv6Addr),
}
```

This code illustrates that we can any kind of data inside an enum variant: strings, numeric types, or structs, for
example. You can even include another enum. Also, standard library types are often not much more complicated that
we might come up with.

Note that even though the standard library contains a definition for `IdAddr`, we can still create and use our
own definition without conflict because we have not brought the standard library’s definition into our scope.

---

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

This enum as four variants with diffrent types. Defining an enum with variant is similar to defining different
kinds of struct definitions, expet the enum does not use the `struct` keyword and all the variants are grouped
together under the `Message` type. The following structs could hold the same data that the preceding enum variants
hold :

```rust
struct QuitMessage; // unit struct
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // tuple struct
struct ChangeColorMessage(i32, i32, i32); // tuple struct
```

But if we used the different structs, each of which has its own type, we could not as easily define a function to
take any of these kinds of messages as we could with an enum.
There is one more similarity between enums and structs: just as we are able to define methods on structs using
`impl` we are also able to define methods on enums. Here is a method named `call` that could define on our
`Message` enum :

```rust
impl Message {
    fn call(&self) {
        // Method content
    }
}

let m = Message::Write(String::from("Hello"));
m.call();
```

The content of the method would use `self` to get the value that we called the method on. In this example, we have
created a variable `m` that has the value `Message::Write(String::from("Hello"))`, and that is what `self` will be
in the body of the `call` method when `m.call()` runs.
