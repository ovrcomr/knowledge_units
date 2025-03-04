Every value is of a certain **datatype**. Rust is a statically typed language, where types must be known.

A **scalar** type represent a single value. Rust as four primary scalar types :
- Integer
- Floating-point number
- Boolean
- Character

<br>

---

<br>

An **integer** is a number without fractional component. They can be either signed (`isize`) or usigned (`usize`) :

| Length  | Signed   | Unsigned  |
|---      |---       | ---       |
| 8-bit   | `i8`     | `u8`      |
| 16-bit  | `i16`    | `u16`     |
| 32-bit  | `i32`    | `u32`     |
| 64-bit  | `i64`    | `u64`     |
| 128-bit | `i128`   | `u128`    |
| arch    | `isize`  | `usize`   |

About *signed* numbers :
- Can store `-(2^n-1)` to `2^n-1 - 1` inclusive, where `n` is the number of bit.
- The `isize` depends on the computer architecture.
- Integer literals in any of the forms down below :

| Number literals  | Example      |
|---               |---           |
| Decimal          | 98_222       |
| Hex              | 0xff         |
| Octal            | 0o77         |
| Binary           | 0b1111_0000  |
| Byte (u8 only)   | b'A'         |

`_` can be a *visual separator*, turning `1000000` into `1_000_000`, that is easier to read.

<br>

**Integer overflow**

As an example, `u8` type can store from `0` to `255`. If something bigger than the max value of the range it assigned :

- (Debug Mode) : The compiler checks for integer overflows that cause a program to *panic* (exit with error) at runtime.

- (Release Mode) : Rust do not include checks for integer overflows. It will just performs complement wrapping.
  In short, values greater than the maximum value the type can hold 'wrap around' to the minimum of the value the type can hold.
  In `u8`case, `256` becomes `0`, `257` becomes `1`...
  This behvior will not perform what the program is expected to do because of value wrapping.

To explicitly handle overflow, there is methods provided by the standard library for primitive numeric types :

- Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`.
- Return the `None` value if there is overflow with the `checked_*` method.
- Return the value and a Boolean indicating wether there was overflow with the `overflowing_*` methos.
- Saturate at the value's minimum or maximum values with the `saturating_*` method.

<br>

---

<br>

**Floating-point numbers** (always signed) are numbers with decimal points. Rust floating types are `f32` (single precision) and `f64` (double precision).
The default type is `f64` because on modern CPUs, it is roughly the same speed as `f32` but is capable of more precision.

```rust
let x = 3.0; // f64 by default
let y: f32 = 3.0; // f32 as specified
```

Floating-point numbers are represented according to the **IEEE-754** standard.

<br>

---

<br>

**Numeric operations**

```rust
// Addition
let sum = 5 + 10;

// Subtraction
let difference = 99.5 - 4.3;

// Multiplication
let product = 4 * 30;

// Division
let quotient = 56.7 / 32.2;
let truncated = -5 / 3; // -1 (but is -1.666...)

// Remainder
let remainder = 43 % 5;
```

<br>

---

<br>

**Boolean type** (single bit size)

```rust
let t = true;
let f: bool = false; // With specific type mention
```

The main way to use boolean is through conditionals, such a control flow and loops.

<br>

---

<br>

**Charaecter type**

Rust's most primitive alphabetic type :

```rust
let c = 'z';
let z: char = 'Z';
```

Unlike strings, *characters* :

- Defined using single quotes
- Four bytes in size, represent a unicode scalar value. (from `U+0000` to `U+D7FF` and `U+E000` to `U10FFFF` inclusive.)
