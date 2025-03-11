**String complexity**

<br>

Different programming languages make different choices bout how to present this complexity to the programmer.
Rust has chosen to make the correct handling of `String` data the default behavior for all Rust programs,
which means programmers have to put more thought into handling UTF-8 data up front. This trade-off exposes more
of the complexity of strings than is apparent in other programming languages, but it prevents us from
having to handle errors involving non-ASCII characters later in our development life cycle.

The good news is that the standard library offers a lot of functionality built off the `String` and `&str` types
to help handle these complex situations correclty. Documentation contains useful things such as `contains` for
searching in a string and `replace` for subsituting parts of a string with another string.
