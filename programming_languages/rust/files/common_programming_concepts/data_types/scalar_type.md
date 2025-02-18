In Rust, every value is of a certain *datatype*. The first data type subset is the *scalar* one.
As a reminder, Rust is a statically typed language, which means that it must know the type of each variable.

A *scalar* type represent a single value. Rust as four primary scalar types :
- Integer
- Floating-point number
- Boolean
- Character

---

**Integer types**

An *integer* is a number without fractional component. They can be either signed (isize) or usigned (usize) :

| Length  | Signed | Unsigned |
|---      |---     | ---      |
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u 128    |
| arch    | isize  | usize    |

*Signed* or *unsigned* refers to the possibilty of the stored number to be negative. If signed, it can, if unsigned, it is not.
Signed numbers are stored using few complement representations :
- Each signed variant can store `-(2^n-1)` to `2^n-1 - 1` inclusive, where `n` is the number of bit.
- The `isize` depends on the computer architecture.
- Integer literals in any of the forms down below :

| Number literals  | Example      |
|---               |---           |
| Decimal          | 98_222       |
| Hex              | 0xff         |
| Octal            | 0o77         |
| Binary           | 0b1111_0000  |
| Byte (u8 only)   | b'A'         |

It's also possible to use `_` as a *visual separator*, turning `1000000` into `1_000_000`, that is easier to read.

<br>

**Integer overflow**

As an example, `u8` type can store from `0` to `255`. If a developer attempt to assign a number out of the type's range (e.g. 300),
*integer overflow* will occurs , which can result in one of two behaviors :

- When compiling in debug mode, Rust compiler checks for integer overflows that cause a program to *panic* at runtime if this behvior occurs.
  Rust uses the term *panick* when a program exit with an error.

- When compiling in release mode, Rust do not include checks for integer overflows. Instead, if it occurs, it will performs two's complement wrapping.
  In short, values greater than the maximum value the type can hold 'wrap around' to the minimum of the value the type can hold.
  In that case, `256` becomes `0`, `257` becomes `1`...
  This behvior will not perform what the program is expected to do because of value wrapping.

To explicitly handle the possibility of overflow, it is possible to use these families of methods provided by the standard library for
primitive numeric types :

  - Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`.
  - Return the `None` value if there is overflow with the `checked_*` methods.
  - Return the value and a Boolean indicating wether there was overflow with the `overflowing_*` methods.
  - Saturate at the value's minimum or maximum values with the `saturating_*` methods.

---

**Floating-point types**

Rust also have two primitive types for *floating-point numbers*, which are numbers with decimal points. Rust floating types are `f32` and `f64`.
The default type is `f64` because on modern CPUs, it is roughly the same speed as `f32` but is capable of more precision. **All floating points are signed**.

```rust
fn main() {

    let x = 3.0; // f64 by default
    let y: f32 = 3.0; // f32 as specified

}
```

Floating-point numbers are represented according to the **IEEE-754** standard. `f32` is single precision float and `f64` is double precision float.

---

**Numeric operations**

- Addition
- Subtraction
- Multiplication
- Division
- Remainder

```rust
fn main() {

    // Addition
    let sum = 5 + 10;

    // Subtraction
    let difference = 99.5 - 4.3;

    // Multiplication
    let product = 4 * 30;

    // Division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // -1

    // Remainder
    let remainder = 43 % 5;

}
```

---

**Boolean type**

Two possible values : `true` or `false`. This is a single bit size :

```rust
fn main() {

    let t = true;
    let f: bool = false; // Example with specific type annotation

}
```

The main way to use boolean is through conditionals, such a control flow and loops.

---

**Charaecter type**

Rust's most primitive alphabetic type :

```rust
fn main() {

    let c = 'z';
    let z: char = 'Z';

}
```

Unlike strings, single quotes `''` are used to declare *characters*. This type is four bytes in size and represent a unicode scalar value.
It means that it can represent much more than ASCII : e.g. Korean characters, emojis and zero width space.
Unicode scalar values range from `U+0000` to `U+D7FF` and `U+E000` to `U10FFFF` inclusive.
