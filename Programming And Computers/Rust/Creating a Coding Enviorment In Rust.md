	This will go over how to start and run a project in rust:

## Downloading Rust:

To start working in rust you will need to download it. If your on a unix based system(e.g. Macos, a Linux Distro) you can run this into your cmd:

```bash
$ curl https://sh.rustup.rs -sSf | sh
```

Installing on Windows is nearly as easy: download and run [rustup-init.exe](https://win.rustup.rs). It will start the installation in a console and present the above message on success.

To ensure that rust is rust is installed run:

```bash
$ rustc --version
```

You should see the version number, commit hash, and commit date. If you don't go [here](https://doc.rust-lang.org/1.30.0/book/first-edition/getting-started.html) for troubleshooting info.

Uninstalling also uses the command line:

```bash
$ rustup self uninstall
```

## Creating A Project Using Cargo:

To start a project in rust we will use Cargo. Cargo is a built in package and system manager that comes  with rust. This will help you manage you project for you. It can do many things such as building your code, downloading the libraries your code depends on, and building those libraries. To ensure that Cargo is installed you can run:

```bash
$ cargo --version
```

You should see the version number, commit hash, and commit date. If theres an error such as `command not found` you may need to reinstall or troubleshoot.

To create a project you can run this command in your shell:

```bash
$ cargo new project_name
```

It has also initialized a new Git repository along with a _.gitignore_ file. Git files won’t be generated if you run `cargo new` within an existing Git repository; you can override this behavior by using `cargo new --vcs=git`.

You can change `cargo new` to use a different version control system or no version control system by using the `--vcs` flag. Run `cargo new --help` to see the available options.

If you open you Cargo.toml file it should look like this:

```toml
[package]
name = "project_name"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]

```

The first line, `[package]`, is a section heading. It indicates that the following lines are configuring a package. As we add more information to this file, we’ll add other sections.

The next three lines set the configuration information Cargo needs to compile your program: the name, the version, and the edition of Rust to use.

The last line, `[dependencies]`, is the start of a section for you to list any of your project’s dependencies. In Rust, packages of code are referred to as _crates_. We won’t need any other crates for this project, but we will in the first project in Chapter 2, so we’ll use this dependencies section then.

Now if you open src/main/main.rs it should look like this:

```rust
fn main() {
     println!("Hello, world!");
}
```

Cargo has automatically created a "Hello, world!" file for you. 

Cargo expects your source files to live inside the _src_ directory. The top-level project directory is just for README files, license information, configuration files, and anything else not related to your code. Using Cargo helps you organize your projects. There’s a place for everything, and everything is in its place.

Building and running code with cargo is very simple. To compile your code enter the following command into your terminal:

```bash
$ cargo build
   Compiling project_name v0.1.0 (file:///projects/project_name)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

This builds an exicutable bianary file that anyone can run. To run your code just run the file:

```bash
$ ./target/debug/project_name
```

We can also use `cargo run` to compile the code and then run the resultant executable all in one command:

```bash
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
     Running `target/debug/project_name`
Hello, world!
```

Using `cargo run` is more convenient than having to remember to run `cargo build` and then use the whole path to the binary, so most developers use `cargo run`.

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn’t produce an executable:

```bash
$ cargo check
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
```

Using `cargo check` is much faster than `cargo build` and is a great way to check if your code is working without having to compile all your code. If you’re continually checking your work while writing the code, using `cargo check` will speed up the process of letting you know if your project is still compiling. 

If you want to build a release you can use  `cargo build --release` to compile your code with optimizations. If you’re benchmarking your code’s running time, be sure to run `cargo build --release` and benchmark with the executable in _target/release_. 

With simple projects, Cargo doesn’t provide a lot of value over just using `rustc`, but it will prove its worth as your programs become more intricate. Once your program gets more complicated its much easier to let Cargo manage it. 

```bash
$ git clone example.org/someproject
$ cd someproject
$ cargo build
```

For more information about Cargo, check out [its documentation](https://doc.rust-lang.org/cargo/).

After creating a working environment to develop your rust code you may want to start by looking into to [[Variables]], [[Data Types]], and [[Functions]].