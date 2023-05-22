Using info I learned from studying error handling, modules, and more heres a basic login reader I wrote:

```rust
//main.rs
use std::collections::HashMap;

pub mod login;

fn main() {
	
	let mut login_map: HashMap<String, String> = HashMap::new();
	
	login_map.insert(String::from("Teddy"), String::from("12345"));
	login_map.insert(String::from("John"), String::from("54321"));
	
	let login_result = match login::login(&login_map, 0) {
		Ok((x, y)) => {
			println!("Hello, {}", x);
			Ok((x, y))
		},
		Err(e) => {
			print!("{}", e);
			Err(e)
		},
	};
}
```

```rust
//login.rs
use std::{io::{self, Error}, collections::HashMap};

fn get_username() -> String {
	
	let mut username = String::new();
	let x = std::io::stdin().read_line(&mut username).unwrap();
	
	username
}


pub fn login(login_map: &HashMap<String, String>, attempt: i32) -> Result<(String, String), io::Error> {
	
	println!("Username:");
	let username = get_username();
	
	println!("Password:");
	let mut password = String::new();
	std::io::stdin().read_line(&mut password).unwrap();
	password = password.trim().to_string();
	
	let correct_password: String = match login_map.get(&username.trim().to_string()){
		Some(x) => x.to_string(),
		None => "NO INPUT".to_string(),
	};
	  
	
	if password.eq(&correct_password.trim().to_string()) {
		Ok((username, password))
	} else {
		println!("Invalid Login, ");
		if attempt < 4 {
			print!("You have {} attempts left.", 4 - attempt);
			login(login_map, attempt + 1)
		} else {
			Err(Error::new(io::ErrorKind::InvalidInput, "You have no more attempts."))
		}
	}
}
```

If you run this code you'll get an output saying:

```console
Username:
```

This is then prompting for a username such as `Teddy`:

```console
Username:
Teddy
Password:
12345
Hello, Teddy
```

This is a successful login however if we enter and invalid login it will give us 5 attempts to enter a correct one:

```console
Username:
Teddy
Password:
54321
Invalid Login,
You have 4 attempts left.
Username:
```

Once you run out of attempts it will say:

```
Invalid Login, You have no more attempts.
```

and the program will end.