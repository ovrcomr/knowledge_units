**Recoverable errors with Result**

<br>

Most errors aren't serious enough to require the program to stop entirely. Sometimes when a function fails
it's for a reason that we can easily interpret and respond to. For example, if you try to open a file and that
operation fails because the file doesn't exist, we might want to create the file instead of terminating the process.

Recall that the `Result` enum is defined as having two variants, `Ok` and `Err`, as follows :

```rust
enum Result<T, E> {
    Ok(T),
    Err(E)
}
```

The `T` and `E` are generic type parameter. What we need to know right now is that `T` represents the type of the value
that will be returned in a success case within the `Ok` variant, and `E` represents the type of the error that will be
returned in a failure case within the `Err` variant. Because `Result` has these generic type parameters, we can use
the `Result` type and the functions defined on it in many different situations where the success value and error value
we want to return may differ.

Let's call a function that returns a `Result` value because the function cloud fail :

```rust
use std::fs::File;

fn main() {
    let gretting_file_result = File::open("hello.txt");
}
```

The return type of `File::open` is a `Result<T, E>`. The generic parameter `T` has been filled in by the implementation of
`File::open` with the type of the success value, `std::fs::File`, which is a file handle. The type of `E` used in the error
value is `std::io::Error`. This return type means the call to `File::open` might succeed and return a file handle that we
can read from or write to. The function call also might fail : for example, the file might not exist, or we might not have
the permission to access the file. The `File::open` function needs to have a way to tell us whether it succeeded or failed
and at the same time give us either the file handle or error information. This information is exaclty what the `Result` enum
conveys.

In the case where `File::open` succeeds, the value in the variable `greeting_file_result` will an instance of `Ok` that contains
a file handle. In the case where it fails, the value in `greeting_file_result` will be an instance of `Err` that contains more
information about the kind of error that occured.

We need to add to the code to take different actions depending on the value `File::open` returns :

```rust
use std::fs::File;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {error:?}"),
    };
}
```

Note that, like the `Option` enum, the `Result` enum and its variants have been brought into scope by the prelude, so we
don't need to specify `Result::` before the `Ok` and `Err` variants in the `match` arms.

When the result is `Ok`, this code will return the inner `file` value out of the `Ok` variant, and we then assign that file
handle to the variable `greeting_file`. After the `match`, we can use the file handle for reading or writing.

The other arm of the `match` handles the cases where we get an `Err` value from `File::open`. In this example, we have chosen
to call the `panic!` macro. If there is no file named *hello.txt* in our current directory and we run this code, we'll see
the following output from the `panic!` macro :

```bash
$ cargo run
   Compiling error-handling v0.1.0 (file:///projects/error-handling)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.73s
     Running `target/debug/error-handling`
thread 'main' panicked at src/main.rs:8:23:
Problem opening the file: Os { code: 2, kind: NotFound, message: "No such file or directory" }
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

<br>

---

<br>

**Matching on different erros**

<br>

From now, the code will `panic!` no matter why `File::open` failed. However, we want to take different action for different
failure reasons. If `File::open` failed because the file doesn't exist, we want to create the file and return the handle to
the new file. If `File::open` failed for any other reason--for example, becaues we didn't have permission to open the file,
we still want the code to `panic!` in the same way it did. For this, we ass an inner `match` expression :

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {e:?}"),
            },
            other_error => {
                panic!("Problem opening the file: {other_error:?}");
            }
        },
    };
}
```

The type of the value that `File::open` returns inside the `Err` variant is `io::Error`, which is a struct provided by the
standard library. This struct has a method `kind` that we call to get an `io::ErrorKind` value. The enum `io::ErrorKind`
is provided by the standard library and has variant we want to use is `ErrorKind::NotFound`, which indicates the file we're
trying to open doesn't exist yet. So we match on `gretting_file_result`, but we also have an inner match on `error.kind()`.

The condition we want to check in the inner match is whether the value returned by `error.kind()` is the `NotFound` variant
of the `ErrorKind` enum. If it is, we try yo create the file with `File::create`. However, because `File::create` could also
fail, we need a second arm in the inner `match` expression. When the file can't be created, a different error message is
printed. The second arm of the outer `match` stays the same, so the program panics on any error besides the missing file error.

<br>

---

<br>

*Alternatives to using match with `Result<T, E>`*

<br>

The `match` expression is very useful but also very much a primitive. Closures are used with many of the methods defined
on `Result<T, E>`. These methods can be more concise than using `match` when handling `Result<T, E>` values in our code.

For example, here is another way to write the same logic, this time using closures and the `unwrap_or_else` method :

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap_or_else(|error| {
        if error.kind() == ErrorKind::NotFound {
            File::create("hello.txt").unwrap_or_else(|error| {
                panic!("Problem creating the file: {error:?}");
            })
        } else {
            panic!("Problem opening the file: {error:?}");
        }
    });
}
```

Although this code has the same behavior, it doesn't contain any `match` expressions and is cleaner to read.

<br>

---

<br>

*Shortcuts for panic on error : unwrap and expect*

<br>

Using `match` works well enough, but it can be a bit verbose and it doesn't always communiate intent well. The `Result<T, E>`
type has many helper methods defined on it to do various, more specific tasks. The `unwrap` method is a shortcut method
implemented just like the `match` expression. If the `Result` value is the `Ok` variant, `unwrap` will return the value
inside the `Ok`. If the `Result` is the `Err` variant, `unwrap` will call the `panic!` macro for us :

```rust
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap();
}
```

If we run this code wihtout a *hello.txt* file, we will see an error message from the `panic!` call that the `unwrap` method makes :

```bash
thread 'main' panicked at src/main.rs:4:49:
called `Result::unwrap()` on an `Err` value: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

Similarly, the `expect` method lets us also choose the `panic!` error message. Using `expect` instead of `unwrap` and providing
good error messages can convey our intent and make tracking down the source of a panic easier. The syntax of `expect` looks like :

```rust
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt")
        .expect("hello.txt should be included in this project");
}
```

We use `expect` in the same way as `unwrap` : to return the file handle or call the `panic!` macro. The error message used by `expect`
in its call to `panic!` will be the parameter that we pass to `expect`, rather than the default `panic!` message that `unwrap` uses :

```bash
thread 'main' panicked at src/main.rs:5:10:
hello.txt should be included in this project: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

In production-quality code, most developers choose `expect` rather than `unwrap` and give more context about why the operation is expected
to always succeed. That way, if your assumptions are ever proven wrong, you have more information to use in debugging.
