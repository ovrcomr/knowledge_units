**Loops** are a way to execute a block of code several times.

```rust
loop { // Infinite loop
    println!("Again");
}
```

<br>

---

<br>

**Returning values from loops**

Loops can be combined with conditionals, to perform a task, and the result can be assigned to a variable :

```rust
let mut counter = 0;

let result = loop { // result will be equal to 20
    counter += 1;

    if counter == 10 {
        break counter * 2;
    }
};
```

<br>

---

<br>

**Loop labels**

`break` and `continue` are applied by default to the inner most loop when called.
*Labels* allows to call `break` or `continue` for a targeted loop :

```rust
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
```

<br>

---

<br>

**Conditional loop : while**

`while` loop has an integrated condition that the loop refers to. (unlike `loop` that require `break`).

```rust
let mut counter = 0;
let goal = 10;

while counter < goal {
    counter += 1;
}
```

<br>

---

<br>

**Loop over collection : for**

`for` is a safer way to iterate over a collection, since it will not try to access an unexisting element (that cause the program to panic).

```rust
let people = ["Paul", "Marie", "Andrew"];

for name in people {
    println!("{}", name);
}
```

`for` also entails to run the code a finite and predeterminate amout of time, unlike the `while` that can be infinite :

```rust
for number in (1..4).rev() { // is for reverse the range
    println!("{number}");
}

println!("{Go!}");
```
