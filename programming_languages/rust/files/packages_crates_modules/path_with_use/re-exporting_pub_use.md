**Re-exporting names**

<br>

When bringing a name into scope with `use`, the name available in the new scope is private. To enable the code
that calls our code to refer to that as if it had been defined in that code's scope, we can combine `pub` and
`use`. This technique is called *re-exporting* because we are bringing an item into scope but also making that
item available for others to bring into their scope :

<br>

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

<br>

Before this change, external code would have to call the `add_to_waitlist` function by using the path
`restaurant::front_of_house::hosting::add_to_waitlist()`, which also would have required the `front_of_house`
module to be marked as `pub`. Now that is `pub use` has re-exported the `hosting` module from the root module,
external code can use the path `restaurant::hosting::add_to_waitlist()` instead.

Re-exporting is useful when the internal structure of your code is different from how programmers calling your
code would think about the domain. For example, in this restaurant metaphor, the people running the restaurant
think about "front of house" and "back of house". But customers visiting a restaurant probably won't think about
the parts of the restaurant in those terms. With `pub use`, we can write our code with one structure but expose
a different structure. Doing so makes our library well organized for programmers working on the library and
programming calling the library.
