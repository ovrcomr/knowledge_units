**Choosing when to panic**

<br>

When code panics, there is no way to recover. We could call `panic!` for any error situation, whether there's
a possible way to recover or not, but then we are making the decision that a situation is unrecoverable on
behalf of the calling code. When choosing to return a `Result` value, we give the calling code options.
The calling code could choose to attempt to recover in an appropriate way regarding the situation, or it
could decide that an `Err` value in this case is unrecoverable, so it can call `panic!` and turn our
recoverable error into a unrecoverable one. Therefore, returning `Result` is a good default choice
when defining a function that might fail.

In situations such as examples, prototypes code and tests, it is more appropriate to write code that panics
instead of returning a `Result`. First, we will explore why, then discuss situations in which the compiler
can't tell that failure is impossible, but as a human can.

<br>

---

<br>

**Examples, prototype code and tests**

<br>

When we are writing an example to illustrate some concept, also including robust error-handling code can
make the example less clear. In examples, it's understood that a call to a method like `unwrap` that could
panic is meant as a placeholder for the way we would want our application to handle erros, which can
differ based on what the rest of the code is doing.

Similarly, the `unwrap` and `expect` methods are very handy when prototyping, before we are ready to
decide how to handle erros. They leave clear markers in our code for when we are ready to make our program
more robust.

If a method call fails in a test, we would want the whole test to fail, even if that method isn't the
functionality under test. Because `panic!` is how a test is marked as a failure, calling `unwrap` or
`expect` is exactly what should happen.
