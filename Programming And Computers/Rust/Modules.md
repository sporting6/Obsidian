Here's a step-by-step tutorial on how to define, store, and access modules in Rust:

### Defining a Module

To define a module in Rust, you need to use the `mod` keyword followed by the name of the module:

```rust
mod my_module {
    // module contents go here
}
```

You can place a module definition anywhere in your code, but it's common to place them at the top of a file.

### Storing Modules

You can store modules in separate files by creating a new file with the same name as the module and adding the module definition to the file. For example, if you have a module named `my_module`, you can create a file named `my_module.rs` and add the module definition to the file:

```rust
// In my_module.rs
mod my_module {
    // module contents go here
}
```

To use a module from another file, you need to use the `mod` keyword followed by the name of the module and the path to the file:

```rust
mod my_module;
```

This will tell Rust to load the module from the file named `my_module.rs`.

You can also create modules inside of other modules. You can then define their contents either in curly brackets following the mod definition like this:
```rust
//In main.rs
mod my_module {
	mod my_submodule {
		//module contents go here
	}
	//rest of module contents go here
}
```

Or you could store it in a file with the same name as the module, under a folder with the same name as the module that it is defined in. So for the prior example it would be: `src/my_module/my_submodule.rs`.

### Accessing Modules

To access items from a module, you need to use the `use` keyword followed by the name of the module and the name of the item you want to use:

```rust
use my_module::my_function;
```

This will bring the `my_function` [[Functions|functions]] into the current scope so that you can use it directly:

```rust
fn main() {
    my_function();
}
```

If you want to use multiple items from a module, you can use the `use` keyword followed by a list of items separated by commas:

```rust
use my_module::{my_function, MyType};
```

This will bring both the `my_function` function and the `MyType` type into the current scope.

You can also use the `pub` keyword to make items in a module public, which means they can be used by code outside of the module:

```rust
mod my_module {
    pub fn my_function() {
        // function contents go here
    }
}
```

To use a public item from another module, you need to use the `use` keyword followed by the name of the module and the name of the item:

```rust
use my_module::my_function;
```

This will bring the `my_function` function into the current scope so that you can use it directly.

To access a "sub module" you can reference it like this:

```rust
//In main.rs
pub mod my_module {
	pub mod my_submodule {
		pub fn my_function() {
			//Function contents go here
		}
		//Rest of module contents go here
	}
	//Rest of module contents go here
}


fn main() {
	my_module::my_submodule::my_function();
}
```

We can also use the `use` keyword like this:

```rust
use my_module::my_submodule::my_function;
```
