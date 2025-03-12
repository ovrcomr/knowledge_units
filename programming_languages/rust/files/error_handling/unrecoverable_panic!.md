**Unrecoverable errors with panic!**

Sometimes bad things happen in our code, and there is nothing we can do about it. In these cases, Rust has the `panic!` marco.
There are two ways to cause a panic in pratice : by taking an action that causes our code to panic (such as accessing an array past
the end) or by expicitly calling the `panic!` macro. In both cases, we cause a panic in our program. By default, these panics will print
a failure message, unwind, clean up the stack, and quit. Via an environement variable, we can also have Rust display the call stack when
a panic occurs to make it easier to track down the source of the panic.

<br>

*Unwinding the stack or aborting in reponse to a panic*

By default, when a panic occurs, the program starts *unwinding*, which means Rust walks back up the stack and cleans up the data
from each function it encounters. However, walking back and cleaning up is a lot of work. Rust, therefore, allows us to choose the
alternative of immediatly *aborting*, which ends the program without cleaning up.

Memory that the program was using then need to be cleaned up by the operating system. If in our project we need to make the
resultant binary as small as possible, you can switch from unwinding to aborting upon a panic by adding `'panic = 'abort'` to the
appropriate `[profile]` sections in our `Cagro.toml` file. For example, if we want to abort on panic in release mode :

```toml
[profile.release]
panic = 'abort'
```

Calling `panic!` in a simple program with this :

```rust
fn main() {
    panic!("crash and burn");
}
```
```bash
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.25s
     Running `target/debug/panic`
thread 'main' panicked at src/main.rs:2:5:
crash and burn
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

The call to `panic!` causes the error message contained in the last two lines. The first line shows our panic message
and the place in our source code where the panic occured : `src/main.rs:2:5` indicates that it's the second line, fifth
character of the file.

In this case, the line indicated is part of our code, and if we go to that line, we see the `panic!` macro call. In other
cases, the `panic!` call might be in code that our code calls, and the filename and line number reported by the error message
will be someone else's code where the `panic!` marco is called, not the line of our code that enventually led to the `panic!` call.

We can use backtrace of the functions the `panic!` call came from to figure out the part of our code that is causing the problem.
To understand how to use the `panic!` backtrace, let's look at another example and see what it's like when a `panic!` call comes
from a library because of a bug in our code instead of from our code calling the marco direclty :

```rust
fn main() {
    let v = vec![1, 2, 3];

    v[99];
}
```

Here, we are attempting to access the 100th element of our vector, but the vector has only three elements. In this situation,
Rust will panic. Using `[]` is supposed to return an element, but if you pass an invalid index, there's no element that Rust
could return here that would be correct.

In C, attempting to read beyond the end of a data structure is undefined behvior. We might get whatever is at the location in
memory that would correspond to that element in the data structure, even though the memory doesn't belong to that structure.
This is called a *buffer overread* and can lead to security vulnerabilities if an attacker is able to manipulate the index in
such a way as to read data they shouldn't be allowed to that is stored after the data structure.

To protect our program from this sort of vulnerability, if we try to read an element at an index doesn't exist, Rust will
stop execution and refuse to continue. Let's try it and see :

```rust
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.27s
     Running `target/debug/panic`
thread 'main' panicked at src/main.rs:4:6:
index out of bounds: the len is 3 but the index is 99
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

This errors points at line 4 of our *main.rs* where we attempt to acces index `99` of the vector in `v`.

The `note:` line tells us that we can set the `RUST_BACKTRACE` environement variable to get a backtrace
of exactly what happened to cause the error. A *backtrace* is a list of all the functions that have been
called to get to this point. Becktraces in Rust work as they do in other languages: the key to reading the backtrace
is to start from the top and read until you see files we wrote. That is the spot where the problem originated. The
lines above that spot are code that your code has called; the lines below are code that called your code. These before-and-after
lines might include core Rust code, standard library code, or crates that we are using. Let's try getting a backtrace by setting
the `RUST_BACKTRACE` environement variable to any value execpt `0` :

```bash
$ RUST_BACKTRACE=1 cargo run
thread 'main' panicked at src/main.rs:4:6:
index out of bounds: the len is 3 but the index is 99
stack backtrace:
   0: rust_begin_unwind
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/std/src/panicking.rs:662:5
   1: core::panicking::panic_fmt
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/panicking.rs:74:14
   2: core::panicking::panic_bounds_check
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/panicking.rs:276:5
   3: <usize as core::slice::index::SliceIndex<[T]>>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/slice/index.rs:302:10
   4: core::slice::index::<impl core::ops::index::Index<I> for [T]>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/slice/index.rs:16:9
   5: <alloc::vec::Vec<T,A> as core::ops::index::Index<I>>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/alloc/src/vec/mod.rs:2920:9
   6: panic::main
             at ./src/main.rs:4:6
   7: core::ops::function::FnOnce::call_once
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/ops/function.rs:250:5
note: Some details are omitted, run with `RUST_BACKTRACE=full` for a verbose backtrace.
```

The exact output we see might be different depending on our operating system and Rust version. In order
To get backtraces with this information, debug symbols must be enabled. Debugs symbols are enabled by default
when using `cargo build` or `cargo run` without the `--release` flag, as we have here.

In the output of the backtrace points to the line in our project that's causing the problem : line 4.
If we don't want our program to panic, we should start our investigation at the location pointed to by the first
line mentioning a file we wrote. Where we deliberately wrote code that would panic, the way to fix the panic is to
not request an element beyond the range of the vector indexes. When our code panics in the future, we'll need to
figure out what action the code is taking with what values to cause the panic and what the code should do instead.
