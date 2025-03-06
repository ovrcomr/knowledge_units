**Statements** :  Execute an action without returning a value.

Types of statements:
- Variable declaration `let x = 5;`
- Function definition `fn foo() {}`
- Expression with a semicolon (`x + 1`; turns into () instead of returning a value)

Cannot be nested inside expressions.

<br>
---
<br>

**Expressions** : Always return a value.

Can be nested inside other expressions or statements :
- Function calls: `some_function()`
- Blocks:
  ```rust
  let x = {
      let y = 5;
      y + 1 // Expression: returns 6
  };
  ```
- If-expressions:
  ```rust
  let z = if true { 10 } else { 20 }; // Evaluates to 10
  ```
- Last expression in a block determines its return value (no semicolon).
- Adding a semicolon turns an expression into a statement (x + 1; results in ()).
