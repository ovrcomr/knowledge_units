## **Rust**
<a style="color: grey; font-size: 12" href="./resources.md">Resources</a>

<br>

- Overview - [History](#history) - [Purpose](#purpose)
- Features - [Paradigms](#paradigms) - [Type system](#type-system) - [Memory management](#memory-management) - [Concurrency](#concurrency)
- Ecosystem - [Frameworks](#frameworks) - [Community](#community)
- RW-Application - [Usecases](#usecases) - [Successes](#successes)

<br>

---

<br>

### History

Rust was originally developed by Mozilla Research, with Graydon Hoare starting the project in 2006.
It gained significant traction in 2010 when Mozilla officially sponsored it. The first stable release,
Rust 1.0, was launched in 2015. Since then, Rust has grown rapidly, with consistent community-driven improvements
and widespread industry adoption.

<br>

### Purpose

Rust is primarily designed for systems programming, making it a great alternative to languages like C and C++.
It is used for building web assembly applications, embedded systems, operating systems, game engines, and other
performance-sensitive software. Its memory safety guarantees make it particularly appealing for writing secure and
concurrent applications.

<br>

---

<br>

### Paradigms

- **Procedural programming**: Writing structured and modular code.
- **Functional programming**: First-class functions, immutability, and iterators.
- **Object-oriented programming**: Traits and structs enable modular and reusable code.

<br>

### Type system

- **Statically typed**: Type checking occurs at compile-time, preventing many runtime errors.
- **Strongly typed**: Prevents implicit type conversions that could lead to unintended behavior.

<br>

### Memory management

- **Ownership and Borrowing**: Rust’s unique ownership system ensures memory safety and eliminates data races.
- **No garbage collector**: Unlike languages like Java or Go, Rust does not rely on garbage collection, reducing runtime overhead.
- **Automatic memory deallocation**: The compiler ensures memory is freed when it is no longer needed, using a deterministic approach.

<br>

### Concurrency

- **Threads**: Safe multithreading without data races.
- **Async/Await**: Efficient asynchronous programming for high-performance applications.
- **Message Passing**: Channels for safe inter-thread communication.

<br>

---

<br>

### Frameworks

<span style="color: grey; font-size: 12">Only popular ones are mentioned</span>
- **Rocket & Actix Web**: Web frameworks for building fast and secure applications.
- **Tokio**: Asynchronous runtime for building concurrent applications.
- **Serde**: Serialization/deserialization framework.
- **Diesel & SeaORM**: ORM frameworks for database interactions.

<br>

### Community

- **Forums**: Rust Users Forum : [users.rust-lang.org](https://users.rust-lang.org)
- **Mailing Lists**: Rust Internals and Rust Announcements
- **Conferences**: RustConf, Rust Belt Rust, EuroRust
- **GitHub & Discord**: Strong developer engagement and support channels.

<br>

---

<br>

### Usecases

- **Operating Systems**: Redox OS, a Rust-based operating system.
- **Web Development**: WebAssembly applications and backend services using Rust.
- **Embedded Systems**: IoT devices and real-time systems.
- **Game Development**: Game engines like Bevy and Amethyst.
- **Cryptography & Blockchain**: Used in projects like Solana and Parity Ethereum.

<br>

### Successes

- **Mozilla**: Rust was originally developed for improving the Firefox browser.
- **Dropbox**: Uses Rust for performance-critical parts of its infrastructure.
- **Cloudflare**: Uses Rust for secure networking applications.
- **Microsoft**: Adopting Rust for systems-level programming to enhance security.
- **Amazon Web Services (AWS)**: Uses Rust for performance-critical services like Firecracker.
