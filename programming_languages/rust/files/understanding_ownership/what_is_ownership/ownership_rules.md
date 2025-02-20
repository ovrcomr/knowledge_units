Ownership is a set of rules that govern how a Rust program manages memory.
Some languages have a garbage-collector, seeking for memory that is no longer used.
Some other requires developer to explicitly allocate and free the memory.
Rust uses a third approach, where memory is managed through a system of ownership,
with a set of rules that the compiler checks.

After becoming familiar with Rust ownership, it will be easy to see why it is unique.

---

**Stack and Heap**

Many programming languages don't require to think about the stack and the heap very often.
In systems programming language like Rust, whether a value is on the stack or the heap
affects how the language behaves and why certain decisions from the developer are implied.
Parts of ownership will be described in relation to the stack and the heap later in this chapter,
so here is a brief explanation in preparation.

Many programming languages don’t require thinking about the stack and the heap very often.
However, in a systems programming language like Rust, whether a value is on the stack or
the heap affects the language's behavior and necessitates certain decisions. The concepts
of ownership will be discussed in relation to the stack and the heap later in this
chapter, so a brief explanation is provided here.

Both the stack and the heap are parts of memory available to code at runtime, but
they are structured differently. The stack stores values in the order they are received
and removes them in the opposite order, known as last in, first out. Imagine a stack
of plates: new plates are added to the top, and plates are taken from the top. Adding
data is called pushing onto the stack, and removing data is called popping off the
stack. All data stored on the stack must have a known, fixed size. Data with an
unknown size at compile time or a variable size must be stored on the heap.

The heap is less organized: when data is placed on the heap, a certain amount of
space is requested. The memory allocator finds an empty spot in the heap that is
big enough, marks it as in use, and returns a pointer to that location. This process
is called allocating on the heap. Because the pointer to the heap is a known, fixed
size, it can be stored on the stack, but accessing the actual data requires following
the pointer. Think of being seated at a restaurant: the host finds an empty table that
fits the group and leads them there. Latecomers can ask where the group is seated to
find them.

Pushing to the stack is faster than allocating on the heap because the allocator
never has to search for a place to store new data; that location is always at the
top of the stack. Allocating space on the heap requires more work because the allocator
must find a sufficiently large space and perform bookkeeping for the next allocation.

Accessing data in the heap is slower than accessing data on the stack because a pointer
must be followed. Contemporary processors are faster if they jump around less in memory.
Consider a server taking orders from many tables: it’s most efficient to get all the
orders at one table before moving to the next. Taking orders from multiple tables in
a mixed sequence would be slower. Similarly, a processor works better with data that’
s close to other data, as it is on the stack, rather than farther away, as it can be
on the heap.

When a function is called, the values passed into the function (including pointers
to data on the heap) and the function’s local variables are pushed onto the stack.
When the function is over, those values are popped off the stack.

Keeping track of what parts of code are using data on the heap, minimizing
duplicate data on the heap, and cleaning up unused data to avoid running out of space
are problems that ownership addresses. Understanding ownership means not having to think
about the stack and the heap very often, but knowing that ownership's main purpose is
to manage heap data helps explain its mechanisms.

---

**Ownership rules**

- In Rust, each value has an owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.
