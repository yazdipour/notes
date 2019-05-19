# RUST

```bash
rustc --version
rustup default nightly #enable nightly mode

rustc main.rs #To make exec

cargo new projName #create newProj
cargo run build #build proj

cargo run #build and execute
```

## HelloWorld

```rust
//main.rs
extern create piston_window; //??
use  piston_window;::*; // use lib

fn main(){
	let x = 1.0; // float
	let arr = [1, 0, 2]; //array
	let tup = (5, "ccc"); //tuple
	let (mInt, mString) = tup;

	println!("Hello {}",arr[0]);

	println!(x); // ERROR: x is int, correct form println!("{}",x);
}
fn foo(bar: str){} // ERROR: Doesnt know the Length
fn foo(bar: &str){} // Declear dynamic length

```

## WebServer

```rust
use std::net::TcpListener;

fn main(){
	let listener = TcpListener::bind("127.0.0.1:8000").unwrap();
	for stream in listener.incoming(){
		let stream = steram.unwrap();
		println!("A Connection was made");
	}
}
```