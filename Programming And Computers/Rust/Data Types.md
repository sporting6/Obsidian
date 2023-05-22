In Rust, every value has a data type that informs the computer how to use the data. There are two types of data: scalar and compound. Rust is a statically typed language, meaning it needs to know the variable types during compilation. Often, the compiler can determine the type from the value and how it's used.

In cases when multiple types are possible, such as converting from a string to a number, you have to add a type annotation like this:

```rust
let everything: u32 = "42".parse().expect("Not an Int!");

println!("{everything}");
```

This creates a variable `everything` with the data annotation `i32` which creates a 32bit long integer. This is then set equal to `"42".parse().expect("Not an Int!")`. The `.parse()` parses the string into what data type it needs to be and the `.expect("Not an Int!")` tells it what to say when it doesn't meet that data type's criteria.

if you dont add type annotations you will get an error like this

```console
error[E0282]: type annotations needed
 --> src/main.rs:2:9
  |
2 |     let everything = "42".parse().expect("Not an Int!");
  |         ^^^^^^^^^^
  |
help: consider giving `everything` an explicit type
  |
2 |     let everything: /* Type */ = "42".parse().expect("Not an Int!");
  |                   ++++++++++++
```

## Scalar Types

A Scaler type represents a single value. There are four different main scaler types in rust: integers, floats, booleans, and characters. These are the same as most other programming languages. 

#### Integers:

An integer refers to a numerical value that lacks a decimal component, as exemplified by our [earlier use](#constants) of `u32` to establish a constant. `u32` is an unsigned integer type that requires 32 bits of storage space (signed integer types begin with 'i' instead of 'u'). 

Each variant of the integer type can be signed or unsigned and has a specified size. Signed and unsigned refer to the possibility of the number being negative, requiring a sign to be represented (signed), or only being positive, and therefore, can be represented without a sign (unsigned). This can be likened to writing numbers on paper, where the presence of a plus or minus sign indicates the sign of the number. However, when it's assumed that a number is positive, it's written without a sign. The storage of signed numbers utilizes the two's complement representation.

Each signed variant can store numbers from -(2<sup>n - 1</sup>) to 2<sup>n - 1</sup> - 1 inclusive, where _n_ is the number of bits that variant uses. So an `i8` can store numbers from -(2<sup>7</sup>) to 2<sup>7</sup> - 1, which equals -128 to 127. Unsigned variants can store numbers from 0 to 2<sup>n - 1</sup>, so a `u8` can store numbers from 0 to 2<sup>8</sup> - 1, which equals 0 to 255.

Additionally, the `isize` and `usize` types depend on the architecture of the computer your program is running on, which is denoted in the table as “arch”: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.

Decimal: `98_222`
Hex: `0xff`
Octal: `0o77`
Binary: `0b1111_0000`
Byte (`u8` only): `b'A'`

If a numeric value can belong to multiple types, a type suffix can be added, such as `57u8`, to specify the type. To improve readability, number literals can use the underscore as a visual separator. For example: `1_000` has the same value as `1000`.

For more info about integers and integer overflow go [here](https://doc.rust-lang.org/book/ch03-02-data-types.html#integer-overflow).

#### Floating-Point Numbers:

In Rust, there are two primitive types for representing floating-point numbers, which contain decimal points. The floating-point types in Rust are `f32` and `f64`, corresponding to sizes of 32 bits and 64 bits, respectively. The default type for floating-point numbers is `f64` because, on contemporary CPUs, it offers comparable speed to `f32`, but with increased precision. All floating-point types in Rust are signed. Heres an example:

```rust
let a = 2.5;

let b: f32 = 1.234;
```

Floating-point numbers are represented according to the IEEE-754 standard. The `f32` type is a single-precision float, and `f64` has double precision.

#### Numeric Operations

Rust provides support for standard mathematical operations for all number types, such as addition, subtraction, multiplication, division, and remainder. Integer division truncates towards zero to the nearest integer. The following code exemplifies the usage of each mathematical operation within a let statement:

```rust
let sum = 5 + 10; // addition
let difference = 95.5 - 4.3; // subtraction
let product = 4 * 30; // multiplication
let quotient = 56.7 / 32.2; // division
let remainder = 43 % 5; // remainder
```

For a list of all operators and other symbols go [here](https://doc.rust-lang.org/book/appendix-02-operators.html).

#### Characters

Rust’s `char` type is the language’s most primitive alphabetic type. Here are some examples of declaring `char` values:

```rust
let x = 'x';
let y: char = 'Æ';
let z = '🤯';
```

To denote a `char` literal in Rust, we use single quotes instead of double quotes, which are reserved for `string` literals. Rust's `char` type is four bytes in size and can represent a Unicode Scalar Value, meaning it can represent more than just ASCII characters. Rust's `char` type can also represent accented letters, Chinese, Japanese, and Korean characters, emojis, and zero-width spaces. The range of Unicode Scalar Values in Rust is `U+0000` to `U+D7FF` and` U+E000`  to `U+10FFFF`, inclusive. However, it's worth noting that the concept of a "character" in Unicode is somewhat ambiguous, so the intuition for what a character is may not be consistent with the definition of a `char` in Rust.