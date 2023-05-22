Compound type can group multiple values or [[Data Types]] into one type. Rust has two primitive compound types: tuples and arrays.

## Tuple Types

A tuple is a great way to group multiple values together. They have a fixed length so once declared cannot shrink or expand. 

To create a tuple in Rust, we enclose a comma-separated list of values inside parentheses. Each position within the tuple has a designated type, and the types of the values within the tuple can vary. In the following example, we've included optional type annotations:

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
```

Here, we've created a tuple that includes an `i32`, an `f64`, and a `u8`. The first element of the tuple is of type `i32`, the second element is of type `f64`, and the third element is of type `u8`. 

To extract individual values from a tuple in Rust, we can use pattern matching to destructure the tuple value. Here's an example:

```rust
let tuple = (60, 12.4, 7);

let (x, y, z) = tuple;

println!("The value of y is: {y}");
```

In this example, we've declared a tuple with the values `(500, 6.4, 1)` and assigned it to the variable `tup`. We then use pattern matching to extract the values from the tuple and assign them to the variables `x`, `y`, and `z`. Finally, we print the value of `y`, which will output `6.4` in this case.

You can also extract a specific value from a tuple by using a period followed by the values index:

```rust
let x: (i32, f64, u8) = (60, 12.4, 7);

    let sixty = x.0;

    let twelve_point_four = x.1;

    let seven = x.2;
```

This program creates the tuple `x` and then accesses each element of the tuple using their respective indices. As with most programming languages, the first index in a tuple is 0.

The tuple without any values has a special name, _unit_. This value and its corresponding type are both written `()` and represent an empty value or an empty return type. Expressions implicitly return the unit value if they don’t return any other value.

## Array Types

Using arrays in another way to represent multiple values, however unlike tuples, all the values must be of the same type. Arrays in rust also have a fixed lenght. Here is an example:

```rust
let x = [1, 2, 3, 4, 5];
```

Arrays can be beneficial if you prefer your data to be assigned to the stack rather than the heap or if you require a fixed number of elements. However, they lack the flexibility of [[Vector]] types. Vectors, which are part of the standard library, are a comparable collection type that can expand or contract in size. If you're uncertain which to choose between an array and a vector, it's recommended to opt for a vector.

To define a certian data type it is very simillar to variables however we use square brackes and can also include the length of the array we want:

```rust
let x: [i32, 5] = [1, 2, 3, 4, 5];
```

To set the same value for all elements of an array during initialization, you can indicate the initial value, followed by a semicolon, and then enclose the length of the array in square brackets. An example of this is demonstrated below

```rust
let x = [1; 5];
```

The array named `a` will contain `5` elements that will all be set to the value `1` initially. This is the same as writing `let x = [1, 1, 1, 1, 1];` but in a more concise way.

#### Accessing Elements of an Array

Sence an array is a single memory chunk of known length you can access its entries using indexing like this:

```rust
let x = [1, 2, 3, 4, 5];

let y = x[2];
let z = x[4];
```

Using this we may enter an invalid/out of bounds array index. For example if we run this example from the rust book and enter a value greater than 4:

```rust
use std::io;

fn main() {
    let a = [1, 2, 3, 4, 5];

    println!("Please enter an array index.");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");

    let element = a[index];

    println!("The value of the element at index {index} is: {element}");
}
```

This program will end up panicing and give an error saying: 

```console
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 5', src/main.rs:19:19
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

A runtime error occurred in the program due to an invalid index used in the indexing operation, causing it to end without executing the final println! statement. Rust language protects against accessing invalid memory by checking if the index is within the array length. If it's not, Rust panics to prevent memory access.