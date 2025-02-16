<br>

On *macOs*, open the terminal and use :

```bash
$ curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh
```

The command downloads a script and start the installation of the `rustup` tool, which
install the latest version of Rust. The password of the machine may be required.

```bash
Rust is installed now. Great!
```
A *linker* is also required, which is a program that joins Rust compiled outputs
into a file. If linker errors are shown, install a C compiler, which often include
a linker. Also useful because some common Rust packages depends on C code and will
need a C compiler. Install a C compiler using :

```bash
$ xcode-select --install
```
