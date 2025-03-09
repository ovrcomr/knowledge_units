It is also possible to use `pub` to designate structs and enums as public, but there are few extra details
to the usage :
- If we use `pub` before a struct defintion, we lake the struct public, but the struct's fields remains private.
- We can make eack field public or not on a case-by-case basis.

```rust
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}

pub fn eat_at_restaurant() {
    // Order a breakfast in the summer with Rye toast
    let mut meal = back_of_house::Breakfast::summer("Rye");
    // Change our mind about what bread we'd like
    meal.toast = String::from("Wheat");
    println!("I'd like {} toast please", meal.toast);

    // The next line won't compile if we uncomment it; we're not allowed
    // to see or modify the seasonal fruit that comes with the meal
    // meal.seasonal_fruit = String::from("blueberries");
}
```

Because the `toast` field in the `back_of_house::Breakfast` struct is public, in `eat_at_restaurant` we can write
and read to the `toast` field using dot notation.

Also, because `back_of_the_house::Breakfast` has a private field, the struct needs to provide a public associated
function that constructs an instance of `Breakfast` (`summer` here). If `Breakfast` did not have such a function,
we could not create an instance of it in `eat_at_restaurant` because we could not set the value of the private filed.

In contrast, if we make an enum public, al of its variants are then public. We only need the `pub` before the `enum`.

```rust
mod back_of_house {
    pub enum Appetizer {
        Soup,
        Salad,
    }
}

pub fn eat_at_restaurant() {
    let order1 = back_of_house::Appetizer::Soup;
    let order2 = back_of_house::Appetizer::Salad;
}
```
