Often, it can be useful to execute a block of code more than once. For this task, Rust provides several loops, which will run through the code inside it.

```rust
fn main() {

    loop {
        println!("Again");
    }

}
```

This loop will print `"Again"` indefinitely until stopping the program manually.
By adding conditional statements (if/else) to a loop, it is possible to do more useful things such as :

```rust
fn main() {
    let mut counter: i32 = 0;
    let goal: i32 = 10;

    loop {
        if counter < goal {
            counter += 1;
            println!("Counter is now {counter}");
        } else {
            println!("Counter reached the goal");
            break;
        }
    }
}
```

This loop continue to add one to `counter` while it is smaller than the goal. Here is another case where using loops is useful :

```rust
fn main() {
    let array = ["Paul", "Marie", "Andrew"];
    let mut index = 0;

    loop {
        if index < array.len() {
            println!("{}", { array[index] });
            index += 1;
        } else {
            println!("Everyone as been listed");
            break;
        }
    }
}
```

---

**Returning values from loops**

On of the uses of a loop is to retry an known operation that might fail based on the condition, such as checking wether a thread has completed his job.
This result might also need to be passed to a variable to be stored, to be reused elsewhere in the code :

```rust
fn main() {
    let mut counter: i32 = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

Here, `counter` has been 'returned' because the performed actions, and so, the result of those, is accessible from the `result` variable.

---

**Loop labels to disambiguate between multiple loops**

If multiple loops are nested, `break` and `continue` apply to the innermost loop at that point. It can optionally be specified a loop label, to specify
at which loop a `break` or `continue` is addressed to. Loop labels must begin with a single quote. Here is an example :

```rust
fn main() {

    let mut count: i32 = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining: i32 = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;

    }

    println!("End count = {count}");

}
```

---

**Conditional loops with while**

`while` loops are another way to run a block of code as long as the passed condition is true, it is an simple way to use loop without
being obligated to use `break` or `continue` (it remains possible if needed). It is used to replace the complex `loop` with netsed `if` statements.

```rust
fn main() {

    let mut counter = 0;
    let goal = 10;

    while counter < goal {
        counter += 1;
    }

    println!("Counter = {counter}")

}
```

There is the adapted example using names previously written using `loop` :

```rust
fn main() {
    let array = ["Paul", "Marie", "Andrew"];
    let mut index = 0;

    while counter < array.len() {
        println!("{}", {array[index]});
        index += 1;
    }
}
```

Number of line has been decreased using `while` instead of `loop` and `if/else`.

---

**Looping through a collection with for**

A safer way to retreive data from a collection is to use `for` loops.
As already said, trying to access a collection with an non-existing index causes the compiler to 'panic'.
Using `while` make thise kind of situation less evitable, it is all about uncertainity and precaution.

```rust
fn main() {

    let array = ["Paul", "Marie", "Andrew"];

    for element in array {
        println!("{element}");
    }

}
```

Here, it is sure to avoid any kind of wrong index problem because of the `for` loop.

Using `for` also entails to run the code inside it a finite and predeterminate amout of time, unlike the `while` that can be infinite :

```rust
fn main() {

    for number in (1..4).rev() { // is for reverse the range (not important for the concept)
        println!("{number}");
    }

    println!("{Go!}");
}
```

This countdown use a `for` loop and a `Range` to iterate over. `Range` is provided by the standard library, which generate all numbers
in a sequence starting from one number and ends before the last number (here, (1..4) will make 1, 2 and 3).
