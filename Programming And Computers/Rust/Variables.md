To define a variable we use the `let` keyword. All variables in rust are by default immutable. To make them mutable we use the `mut` keyword. Heres an example:

```rust
let x = 5;

println!("x is equal to {x}")
```

This code creates a new variable `x` that is equal to 5. It will then print out "x is equal to 5". Using curly brackest around x like this: `{x}` makes the system print the value of x even while in the string. However if we try to change what `x` is equal to, like this:

```rust
let x = 5;

x = 4;

println!("x is equal to {x}")
```

This will not work because `x` is by default immutable. You will get a compile error like this:

```console
error[E0384]: cannot assign twice to immutable variable `x`
 --> src/main.rs:4:5
  |
2 |     let x = 5;
  |         -
  |         |
  |         first assignment to `x`
  |         help: consider making this binding mutable: `mut x`
3 |
4 |     x = 4;
  |     ^^^^^ cannot assign twice to immutable variable
```

We must then use the `mut` keyword to make them mutable:

```rust
let mut x = 5;

x = 4;

println!("x is equal to {x}")
```

This will now work and should output `x is equal to 4`. 

## Shadow Variables

Shadowing is where we declare a new variable with the same name as a previous variable. When the second variable is introduced, it becomes the one that the compiler recognizes when the variable name is used, causing the first variable to be shadowed. Essentially, the second variable supersedes the first and will continue to do so until it is shadowed itself or the scope is ended. 

We can shadow a variable by using the same variable’s name and repeating the use of the `let` keyword as follows:

```rust
let x = 5;

let x = x + 1;

    {
        let x = x * 2;
        println!("X in the inner scope is equal to: {x}");
    }

println!("x is equal to: {x}");
```

Initially, the variable `x` is assigned a value of `5`. However, a new variable `x` with a value of `x + 1` is introduced, which shadows the original `x` value. Then, a new scope is created where another variable `x` is declared, which overshadows the previous variable and has a value of `x * 2` or `12`. The program prints out this value in the current scope. Later, the program returns to the original scope where the first shadow variable `x` is printed, which has a value of `x + 1` or `6`.

Shadowing and marking a variable as mutable are not equivalent. Without using `let`, trying to reassign a variable will result in a compile-time error. `let` allows for value transformations while maintaining immutability.

Unlike `mut`, shadowing creates a new variable using the same name. This allows for changing the value's type while retaining the name. For instance, when prompting a user to input the number of spaces between text using space characters, the input can be stored as a number.

```rust
let spaces = "   ";
let spaces = spaces.len();
```

If we did this instead:

```rust
let mut spaces = "   ";
spaces = spaces.len();
```

We get an error thatsays we’re not allowed to mutate a variable’s type:

```console
error[E0308]: mismatched types
 --> src/main.rs:3:14
  |
2 |     let mut spaces = "   ";
  |                      ----- expected due to this value
3 |     spaces = spaces.len();
  |              ^^^^^^^^^^^^ expected `&str`, found `usize`

For more information about this error, try `rustc --explain E0308`.
error: could not compile `project_name` due to previous error
```

## Constants

Constants are like [variables](#variables) but they are always immutable or "constant", however instead of using the keyword `let` we use `const` and the type of the value _must_ be annotated.  We will go over annotations more when we talk about [[Data Types]] Here is an example of a constant:

```rust
const METRIC_LIGHT_SPEED: u32 = 299792458;

const STANDARD_LIGHT_SPEED: u32 = METRIC_LIGHT_SPEED * 3.28;
```

Constants are values that remain unchanged throughout a program's execution within the scope in which they were defined. This feature makes them beneficial for values in the program's domain that multiple parts of the program need to access, such as the maximum points a player can earn or how long the program does somthing.

Using constants to name hardcoded values utilized throughout the program is helpful in explaining the value's purpose to future code maintainers. Additionally, it simplifies future changes to the value as it is only required to be updated in a single location in the code.

See the [Rust Reference’s section on constant evaluation](https://doc.rust-lang.org/reference/const_eval.html) for more information on what operations can be used when declaring constants.
