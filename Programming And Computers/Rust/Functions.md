## What Are Functions?
Functions act a lot like functions in other programming languages. You will use the `fn` keyword to declare new functions. Rust uses snake case for function and [[Variables]] names. This means that all letters are lowercase and words are separated by underlines. Heres an example:

```rust
fn main() {
	println("main");
	
	other_funtion();
}

fn other_funtion() {
	println!("5");
}
```

You call any function you’ve defined by entering its name followed by a set of parentheses. Rust doesn’t care where you define your functions, only that they’re defined somewhere in a scope that can be seen by the caller. 

## Function Parameters

Functions in Rust can have parameters, which are variables that are specified in the function's signature. When calling a function with parameters, you provide it with concrete values, which are technically called arguments. However, people often use the terms "parameter" and "argument" interchangeably to refer to either the variables defined in the function or the values passed in when calling it.

In this iteration of `other_function` we can add a parameter:

```rust
fn main() {
	let x = 5;
	
	other_funtion(x);
}

fn other_funtion(x: i32) {
	println!("x is equal to {x}");
}
```

You can define a function with parameters by adding "[[Variables]]" and their respective [[Data Types]] to the set parentheses after the name of the function. You can then use these parameters throughout your function. When defining more than one parameter we separate them with commas:

```rust
fn main() {
	let a = 5;
	let b = 3.5;
	
	other_funtion(a, b);
}

fn other_funtion(x: i32, y: f64) {
	println!("x is equal to {x}");
	println!("y is equal to {y}");
}
```

## Statements and Expressions

Function bodies in Rust consist of a sequence of statements, which may end with an expression. Although we haven't included an ending expression in the functions we've covered so far, we have seen expressions as part of statements. It's important to understand this distinction because Rust is an expression-based language. Unlike other languages that don't make this distinction, let's explore what statements and expressions are and how they impact function bodies.

- Statements are instructions that perform some action and do not return a value.
- Expressions evaluate to a resultant value. Let’s look at some examples. These are kind of like return statements in other languages

An example of a statement is `let x = 5;`. Assigning a variable a value using the `let` keyword is a statement. Statements do not return values. Therefore, you can’t assign a `let` statement to another variable, as the following code tries to do; you’ll get an error:

```rust
let x = (let y = 10);
```

This will return an error because the statement `let y = 10` doesn't result in anything.

In Rust, expressions are a fundamental building block that evaluates to a value, and they constitute most of the code that you'll write. For instance, a simple math operation like `3 + 8` is an expression that evaluates to the value `11`. Expressions can also be part of statements, as seen where the `6` in the statement `let y = 6;` is an expression that evaluates to the value `6`. Additionally, calling a function or a macro is also an expression. Creating a new scope block with curly brackets is also an expression, for example:

```rust
fn main(){
	let x = {
		let y = 12;
		y / 2
	};
	println!("x is equal to {x}");
}
```

This is the expression:

```rust
{
	let y = 12;
	y / 2
}
```

In this case it returns the value of 6 because a variable is defined in the statement `let y = 12` and the expression `y / 2` returns `12 / 2` or `6`. 

## Functions With Returns

This combines what we learned earlier about [functions](#what%20are%20functions) and [statements and expressions](#statements%20and%20expressions). In Rust, we don't name return values, but we must declare their type after an arrow symbol (`->`). The return value of a function in Rust is equivalent to the value of the final expression in the function's body block. Although you can use the return keyword to exit early from a function and specify a value, most functions in Rust implicitly return the last expression. Here's an example of a Rust function that returns a value:

```rust
fn main() {
	let x = three();
	println!("x is equal to {x}");

}

fn three() -> i32 {
    3
}
```

The `3` in the function `three` can **NOT** have a semicolon because it’s an expression whose value we want to return. Here's another example:

```rust
fn main() {
    let x = plus_one(5);
	
    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```

When executing the following code, `The value of x is: 6` will be printed. However, if we add a semicolon at the end of the line containing `x + 1`, making it a statement instead of an expression, an error will occur:

```rust
fn main() {
    let x = plus_one(5);
	
    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1;
}
```

```console
error[E0308]: mismatched types
 --> src/main.rs:7:24
  |
7 | fn plus_one(x: i32) -> i32 {
  |    --------            ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
8 |     x + 1;
  |          - help: remove this semicolon to return this value

For more information about this error, try `rustc --explain E0308`.
error: could not compile `project_name` due to previous error
```

The primary error message `mismatched types` highlights the fundamental problem with this code. The plus_one function is defined to return an `i32`, but when `x + 1` is turned into a statement, it doesn't evaluate to a value, instead resulting in the unit type, `()`. As a result, nothing is returned, which contradicts the function's definition and leads to an error. To resolve this issue, Rust recommends removing the semicolon, which would change the statement into an expression and resolve the error.