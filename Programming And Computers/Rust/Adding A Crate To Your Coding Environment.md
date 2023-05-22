Once you've [established an environment](Creating%20a%20Coding%20Enviorment%20In%20Rust) in Rust, you might be interested in utilizing third-party crates. A fantastic platform to locate crates is [crates.io](https://crates.io/).

### 1. Using ``Cargo.toml``

The `Cargo.toml` file is used to specify the dependencies of a Rust project. This is the recommended approach to add a crate to Rust, as it is easy and efficient.

Add the crate to your `Cargo.toml` file: Open the `Cargo.toml` file in your project directory and add the name of the crate to the `[dependencies]` section, followed by its version number. For example, to add the popular `serde` crate, you would add the following line:

```
[dependencies]
serde = "1.0"
```

Save the changes and run `cargo build`: Save the changes to the `Cargo.toml` file, then run the command `cargo build`. This will download the crate and add it to your project's dependencies.

### 2. Using Rust code

If you don't want to use the `Cargo.toml` file, you can add a crate to your project by writing Rust code directly. However, this approach is not recommended as it can be error-prone and time-consuming.

Add the `extern crate` statement: To use an external crate in your Rust code, you need to add an `extern crate` statement at the top of your file. For example, to use the `rand` crate, you would add the following line:

```
extern crate rand;
```

Use the crate in your code: After adding the `extern crate` statement, you can use the crate's functionality in your Rust code. For example, to generate a random number using the `rand` crate, you could write:

```
extern crate rand;

use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    let num = rng.gen_range(1..101);
    println!("Random number: {}", num);
}
```

Compile and run your code: Save the changes to your Rust file, then compile and run your code using the `rustc` command. For example, to compile and run the above code, you would run the following commands:

```
$ rustc myfile.rs
$ ./myfile
```

Note that this approach requires you to manually manage the crate's version and updates, which can be time-consuming and error-prone. Therefore, it is recommended to use the `Cargo.toml` file to manage your project's dependencies whenever possible.