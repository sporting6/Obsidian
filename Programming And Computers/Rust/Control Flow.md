## If Expressions

An `if` expression allows you to run a specific block of code only when a condition is met. For example:

```rust
fn main(){
	let x = 5;
	if x < 10 {
		println!("{x} is less than 10");
	} else {
		println!("{x} is greater than or equal to 10");
	}
}
```

All `if` statements start with the keyword `if` which is then proceeded by a boolean statement/condition. In the example the condition is `x < 10` which checks if the variable `x` is less that 10, which in this case is `true`. We put the code we then want to run inside curly brackets after the condition.

You can also "chain" multiple conditions with an `else if` statement, for example:

```rust
fn main() {
	let x = 2;

	if x == 0 {
		println!("x is equal to 0");
	} else if x == 1 {
		println!("x is equal to 1")
	} else if x == 2 {
		println!("x is equal to 2")
	} else if x > 2 {
		println!("x is greater than 2")
	} else {
		println!("x is less than 0")
	}
}
```

This program is should output `x is equal to 2`. This program checks if `x` is equal to `0, 1, 2` and if none of those conditions are met it will check if `x` is greater than `2` and if thats false then it knows that `x` must be less than `0`.

You can also use `if` expressions inside of `let` statement to define a variable like this:

```rust
fn main() {
    let y = true;
    let x = if y { 5 } else { 6 };

    println!("The value of x is: {number}");
}
```

Because `y` is `true`, `x` is then defined as `5`, however if `y` was false `x` would be defined as `6`. 

Both possible definitions for `x` must be of the same [[Data Types]], for example:

```rust
fn main() {
    let y = true;
    let x = if y { 5 } else { "five" };

    println!("The value of x is: {number}");
}
```

This wouldn't work because `5` and `"five"` 