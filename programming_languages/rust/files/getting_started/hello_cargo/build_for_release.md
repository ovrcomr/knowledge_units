There is another command to compile a cargo project :

```bash
$ cargo build --release
```

This will, in a way, optimize the code and make it faster.
The upfront compiling time will be a bit longer, but it will ensure best performances.
This is necesseray for a release to be clean and fast.

The associated executable file will be created in `target/release` instead of the
usual `target/debug`.

In comparaison, the other simple `cargo build` is more for debugging purposes,
and faster to compile, ideal for testing (but not for release).
