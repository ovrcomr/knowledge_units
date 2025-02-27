Rust has an extremely powerful control flow construct called `match` that allows us to compare a value
against a series of patterns and then execute code based on which pattern matches. Patterns can be made up of
literal values, variable names, wildcards, and many other things. The power of `match` comes from the
expressiveness of the patterns and the fact that the compiler confirms that all possible cases are handled.

Think of a `match` expression as being like a coin-sorting machine. Speaking of coins, let's use them as an
example using `match!`. We can write a function that takes an unknown US coin and, in similar way as the
couting machine, determines which coin it is and returns its value in cents :

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

First, we list the `match` keyword followed by an expression, which in this case is the value `coin`.
This seems very similar to a conditional expression used with `if`, but there is a big difference : with
`if`, the condition needs to evalute to a Boolean value but here it can be any type. The type of `coin` in
this example is the `Coin` enum that we defined on the first line.

Next are the `match` arms. An arm has two parts: a pattern and some code. The first arm here has a pattern
that is the value `Coin::Penny` and then then `=>` operator that separates the pattern and the code to run.
The code in this case is just the value `1`. Each arm is separated from the next with a comma.

When the `match` expression executes, it compares the resultant value against the pattern of each arm, in order.
If a pattern mathces the value, the code associated with that pattern is executed. If that pattern does not
match the value, execution continues to the next arm, much as in a coin-sorting machine. We can have as many arms
as we need.

The code associated with each arm is an expression, and the resultant value of the expression in the matching arm
is the value that gets returned for the entire `match` expression.

We don't typically use curly braces if the match arm code is short, If we want to run multiple lines of code in a
`match` arm, we must use curly braces, and the comma following the arm is then optional. For example, the
following code prints "Lucky penny!" every time the method is called with a `Coin::Penny`, but still returns
the last value of the block, `1`:

```rust
fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

---

**Patterns that bind to values**

Another useful feature of match arms is that thay can bind to the part of the values that match the pattern.
This is how we can extract values out of enum variants.

As an example, let's change one of our enum variants to hold data inside it. From 1999 through 2008, the US
minted quarters with different designs for each of the 50 states on one side. No other coins got state designs,
so only quarters have this extra value. We can add this information to out `enum` by changing the `Quarter`
variant to include u `UsState` value stored inside it :

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}
```

Let's imagine that a friend is trying to collect all 50 state quarters. While we sort our loose change coin type,
we will also call out the name of the state associated with each quarter so that if it is one our friend
does not have, they can add it to their collection.

In the match expression for this code, we add a variable called `state` to the pattern that matches values of the
variant `Coin::Quarter`. When a `Coin::Quarter` matches, the `state` variable will bind to the value of that
quarter's state. Then we can use `state` in the code for that arm, like so :

```rust
fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {state:?}!");
            25
        }
    }
}
```

If we were to call `value_in_cents(Coin::Quarter(UsState::Alaska))`, `coin` would be `Coin::Quarter(UsState::Alaska)`.
When we compare that value with each of the match arms, none of them match unitl we reach `Coin::Quarter(state)`.
At that point, the binding for `state` will be the value `UsState::Alaska`. We can then use that binding in the
`println!` expression, thus getting the inner state value out of the `Coin` enum variant for `Quarter`.
