**Error-handling guidelines**

<br>

It is advisable to have our code to panic when it is possible that our code could end up in a bad state.
In this context, a *bad state* is when some assumption, guarantee, contract, or invariant has been broken,
such as when invalid values, contradictory values, or missing values are passed to our code :

- The bad state is something that is unexpected, as opposed to something that will likely happen occasionally,
  like a user entering data in the wrong format.

- Our code after this point needs to rely on not being in this bad state, rather than checking for the problem
  at every step.

- There is not a good way to encode this information in the types we use.

If someone calls our code and passes in values that don't make sense, it's best to return an error if we can
so the user of the library can decide what they want to do in that case. However, in cases when continuing
could be insecure or harmful, the best choice might be to call `panic!` is often appropriate if we are calling
external code that is out of our control and it returns an invalid state that we cannot fix.

However, when failure is expected, it is more appropriate to return a `Result` than to make a `panic!` call.
Examples include a parser being given malformed data or an HTTP request returning a status that indicates we
have hit a rate limit. In these cases, returning a `Result` indicates that failure is an expected possibility
that the calling code must decide how to handle.

When our code performsan operation that could put a user at risk if it is called using invalid values,
our code should verify the values are valid first and panic if the value are not valid. This is mostly
for safety reasons : attempting to operate on invalid data can expose our code to vulnerabilities. This is
the main reason the standard library will call `panic!` if we attempt an out-of-bounds memory access : trying
to access memory that doesn't belong to the current data structure is a common security problem. Functions often
have *contracts* : their behavior is only guaranteed if the inputs meet particular requirements. Panicking
when the contract is violated makes sense because a contract violation always indicates a caller-side bug, and
it is not a kind of error we want the calling code to have to explicitly handle. In fact, there is no
reasonable way for calling code to recover; the calling *programmers* need to fix the code. Contracts for a
function, especially when a violation will cause panic, should be explained in the API documentation for the
function.

However, having lots of errors checks in all of our functions would be verbose and annoying. Fortunately, we can
use Rust's type system (and thus the type checking done by the compiler) to do many of the check for us.
If our function has a particular type as a parameter, we can proceed with our code's logic knowing that the
compiler has already ensured we have a valid value. For example, if we have a type rather than an `Option`,
our program expects to have *something* rather than *nothing*. Our code then doesn't have to handle two
cases for the `Some` and `None` variants : it will only have one case for definitly having a value. Code trying
to pass nothing to our function won't even compile, so our function doesn't have to check for that case at
runtime. Another example is using an unsigned integer type such as `u32`, which ensures the parameter is never
negative.
