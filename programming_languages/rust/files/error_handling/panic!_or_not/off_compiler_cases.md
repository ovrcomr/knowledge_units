**Cases in which we may have more information that the compiler**

<br>

It would also be appropriate to call `unwrap` or `expect` when we have some other logic that ensures the
`Result` will have an `Ok` value, but the logic isn't something the compiler understands. We will still
have a `Result` value that we nedd to handle : whatever operation we are calling still has the possibility
of failing in general, even though it's logically impossible in our particular situation. If we need to
ensure by manually inspecting the code that we well never have a `Err` variant, it's perfectly acceptable
to call `unwrap`, and even better to document the reason we think we'll have an `Err` variant in the
`expect` text :

<br>

```rust
use std::net::IpAddr;

let home: IpAddr = "127.0.0.1"
    .parse()
    .expect("Hardcoded IP address should be valid");

```

<br>

We are creating an `IpAddr` instance by parsing a hardcoded string. We can see that `127.0.0.1` is a valid
IP address, so it's acceptable to use `expect` here. However, having a hardcoded, valid string doesn't change
the return type of the `parse` method : we still get a `Result` value, and the compiler will still make
us handle the `Result` as if the `Err` variant is a possibility because the compiler insn't smart enough
to see that this string is always a valid IP address. If the IP address string came from a user rather
than being hardcoded into the program and therefore *did* have a possibility of failure, we would definitly
want to handle the `Result` in a more robust way instead. Mentioning the assumption that this IP address
is hardcoded will prompt us to change `expect` to better error-handling code, if in the future, we need
to get the IP address from some other source instead.
