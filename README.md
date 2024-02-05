# Rust for Beginners

Welcome to the world of Rust! Whether you're just getting started or looking to refresh your knowledge, this guide will take you through the basics step by step.

## Hello World
Let's kick things off with the classic "Hello, World!" program. Open your Rust file and type:

```rust
fn main() {
    println!("Hello, World!");
}
```

This simple program prints the famous greeting to the console.

## Variables
Rust is statically typed, meaning you must declare the type of your variables. Here's an example:

```rust
fn main() {
    let x = 5;
    let y: i32 = 10;
    let z = x + y;
    println!("Sum: {}", z);
}
```

Learn how to declare variables and perform basic arithmetic operations.

## Working With Strings
Strings in Rust can be manipulated and combined. Explore string operations with this code:

```rust
fn main() {
    let greeting = String::from("Hello");
    let name = "World";
    let message = format!("{}, {}!", greeting, name);
    println!("{}", message);
}
```

## Working With Numbers
Perform operations on numbers in Rust:
```rust
fn main() {
    let a = 5;
    let b = 2;
    let sum = a + b;
    let product = a * b;
    println!("Sum: {}, Product: {}", sum, product);
}
```

## Getting Input From Users
Learn how to get user input with Rust:

```rust
use std::io;

fn main() {
    println!("Enter your name:");
    let mut name = String::new();
    io::stdin().read_line(&mut name).expect("Failed to read line");
    println!("Hello, {}!", name.trim());
}
```

## Arrays
Explore arrays in Rust:

```rust
fn main() {
    let numbers = [1, 2, 3, 4, 5];
    for num in &numbers {
        println!("Number: {}", num);
    }
}
```

## Functions 
Define functions and call them:

```rust
fn add(x: i32, y: i32) -> i32 {
    x + y
}

fn main() {
    let result = add(3, 5);
    println!("Sum: {}", result);
}
```

## For Loop
Iterate through a range of numbers:

```rust
fn main() {
    for i in 1..=5 {
        println!("Number: {}", i);
    }
}
```

## While  Loop
Implement a simple while loop:

```rust
fn main() {
    let mut count = 0;
    while count < 5 {
        println!("Count: {}", count);
        count += 1;
    }
}
```

## Try / Except
Handle errors with Rust's Result type:

```rust
fn main() {
    let result = "42".parse::<i32>();
    match result {
        Ok(num) => println!("Parsed number: {}", num),
        Err(_) => println!("Failed to parse"),
    }
}
```

## Reading Files
Read content from a file:

```rust
use std::fs::File;
use std::io::prelude::*;

fn main() -> std::io::Result<()> {
    let mut file = File::open("example.txt")?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    println!("File content: {}", contents);
    Ok(())
}
```

## Writing to Files
Write to a file in Rust:

```rust
use std::fs::File;
use std::io::prelude::*;

fn main() -> std::io::Result<()> {
    let mut file = File::create("output.txt")?;
    file.write_all(b"Hello, Rust!")?;
    Ok(())
}
```

## Structs
Define a simple struct in Rust:

```rust
struct Dog {
    name: String,
    age: u8,
}

fn main() {
    let my_dog = Dog {
        name: String::from("Buddy"),
        age: 3,
    };

    println!("Dog's name: {}", my_dog.name);
    println!("Dog's age: {}", my_dog.age);
}
```

## Structs with Methods
While Rust doesn't have traditional classes, you can achieve similar functionality with structs and methods:

```rust
struct Dog {
    name: String,
    age: u8,
}

impl Dog {
    fn new(name: &str, age: u8) -> Dog {
        Dog {
            name: String::from(name),
            age,
        }
    }

    fn bark(&self) {
        println!("{} says woof!", self.name);
    }
}

fn main() {
    let my_dog = Dog::new("Buddy", 3);
    my_dog.bark();
}
```

Feel free to explore more of Rust's powerful features as you continue your learning journey! Happy coding!

# Practice Project

This simple Rust project is designed for beginners to practice various language features. The program:

1. **User Input:**
   - Receives the user's name and age through standard input.

2. **Structs:**
   - Defines a `Person` struct to represent user data, including name and age.

3. **Basic Math Operations:**
   - Performs basic mathematical operations (sum, product, and square) on the user's age.

4. **Arrays:**
   - Stores the results of the mathematical operations in an array.

5. **File I/O:**
   - Writes both user information and operation results to a file named `output.txt`.

6. **Functions:**
   - Utilizes functions to modularize code for better organization and readability.

This project covers key Rust concepts such as user input, structs, basic operations, arrays, file I/O, and functions. It serves as a practical hands-on exercise for those learning Rust programming.

```rust
use std::io;
use std::fs::File;
use std::io::prelude::*;

struct Person {
    name: String,
    age: u8,
}

fn main() {
    println!("Enter your name:");
    let mut name = String::new();
    io::stdin().read_line(&mut name).expect("Failed to read the name");

    println!("Enter your age:");
    let mut age_input = String::new();
    io::stdin().read_line(&mut age_input).expect("Failed to read the age");
    let age: u8 = match age_input.trim().parse() {
        Ok(num) => num,
        Err(_) => {
            println!("Invalid age. Using 0 as default.");
            0
        }
    };

    let user = Person { name: name.clone(), age };

    let result_array = perform_operations(age);

    welcome_message(&user);

    write_to_file(&user, &result_array);
}

fn welcome_message(person: &Person) {
    println!("Welcome, {}! You are {} years old.", person.name.trim(), person.age);
}

fn perform_operations(age: u8) -> Vec<u8> {
    let sum = age + 5;
    let product = age * 2;
    let square = age.pow(2) as u8;

    println!("Age + 5: {}", sum);
    println!("Age * 2: {}", product);
    println!("Age squared: {}", square);

    vec![sum, product, square]
}

fn write_to_file(person: &Person, results: &Vec<u8>) {
    let mut file = File::create("output.txt").expect("Failed to create the file");

    write!(file, "Name: {}\nAge: {}\n\n", person.name.trim(), person.age).expect("Failed to write to the file");

    write!(file, "Results:\n").expect("Failed to write to the file");
    for (index, result) in results.iter().enumerate() {
        write!(file, "Operation {}: {}\n", index + 1, result).expect("Failed to write to the file");
    }

    println!("The information has been written to the 'output.txt' file.");
}
```