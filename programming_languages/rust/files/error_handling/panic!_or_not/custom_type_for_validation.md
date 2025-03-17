**Creating custom types for validation**

<br>

Let's take the idea of using Rust's type system to ensure we have a vaid value on step further and look creating
a custom type for validation. For the guessing game, we never validated that the user's guess was between
those numbers before checking it against the secret number. We only validated that the guess was positive.
In this case, the consequences were not very dire : our output of "Too high" or "Too low" whould still be
correct. But it would be a useful enhancement to range versus when the user types, for example, letters instead.

One way to do this would be to parse the guess as an `i32` instead of only a `u32` to allow potentially negative
numbers, and then add a check for the number being in range :

<br>

```rust
loop {
    // --snip--

    let guess: i32 = match guess.trim().parse() {
        Ok(num) => num,
        Err(_) => continue,
    };

    if guess < 1 || guess > 100 {
        println!("The secret number will be between 1 and 100.");
        continue;
    }

    match guess.cmp(&secret_number) {
        // --snip--
}
```

The `if` expression checks wether our value is out of range, tells the user about the problem, and calls `continue`
to start the next iteration of the loop and ask for another guess. After the `if` expression, we can proceed
with the comparaison between `guess` and the secret number knowing that `guess` is between `1` and `100`.

However, this is not an ideal solution : if it were absolutely critical that the program only operated on values
between `1` and `100`, and it had many functions with this requirement, having a check like this in every
function would be tedious (and impact performance).

Instead, we can make a new type and put the validation in a function to create an instance of the type rather
than repeating the validation everywhere. That way, it is safe for functions to use the new type in their
signature and confidently use the values they receive :

<br>

```rust
pub struct Guess {
    value: i32,
}

impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {value}.");
        }

        Guess { value }
    }

    pub fn value(&self) -> i32 {
        self.value
    }
}
```

First we define a struct named Guess that has a field named value that holds an i32.
This is where the number will be stored.

Then we implement an associated function named new on Guess that creates instances of Guess values.
The new function is defined to have one parameter named value of type i32 and to return a Guess.
The code in the body of the new function tests value to make sure it’s between 1 and 100.
If value doesn’t pass this test, we make a panic! call, which will alert the programmer who is writing
the calling code that they have a bug they need to fix, because creating a Guess with a value outside
this range would violate the contract that Guess::new is relying on. The conditions in which Guess::new
might panic should be discussed in its public-facing API documentation; we’ll cover documentation conventions
indicating the possibility of a panic! in the API documentation that you create in Chapter 14. If value does
pass the test, we create a new Guess with its value field set to the value parameter and return the Guess.

Next, we implement a method named value that borrows self, doesn’t have any other parameters, and returns an i32.
This kind of method is sometimes called a getter because its purpose is to get some data from its fields and
return it. This public method is necessary because the value field of the Guess struct is private. It’s important
that the value field be private so code using the Guess struct is not allowed to set value directly: code outside
the module must use the Guess::new function to create an instance of Guess, thereby ensuring there’s no way for a
Guess to have a value that hasn’t been checked by the conditions in the Guess::new function.

A function that has a parameter or returns only numbers between 1 and 100 could then declare in its signature
that it takes or returns a Guess rather than an i32 and wouldn’t need to do any additional checks in its body.
