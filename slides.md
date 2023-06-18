---
title: Rust Beginner Workshop
revealOptions:
  transition: 'none'
  highlight-theme: 'github'
---

# Rust Essentials #1

---

## Tooling

- Install (Linux/Unix)
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

- Installer.exe on Windows

----

```sh
 # Sets up a hello world rust project
cargo init #(--lib)

# Debug build
cargo build #(--release)

# Runs debug app
cargo run

# Add dependencies
cargo add axum
cargo add serde --features derive
```

----

```sh
rustup update # Updates rust version (rustc)
rustup target add aarch64-apple-ios # Adds arm64 apple iOS toolchain
cargo build --release --target aarch64-apple-ios # Builds a release version for apple iOS arm64
```

----

Linter and formatter

```sh
cargo clippy
cargo fmt
```

----

Where to search for libraries

- [Crates.io](https://crates.io/)
- [Lib.rs](https://lib.rs/)


----

Where to find useful things

- [Cheats.rs](https://cheats.rs/)
- [The Rust book](https://doc.rust-lang.org/book/)
- [Rust by Example](https://doc.rust-lang.org/stable/rust-by-example/)

----

IDEs

- VSCode:
  - rust-analyzer
  - CodeLLDB (Linux) / MSVC Debug tools (Windows)

- CLion (JetBrains):
  - Rust-Plugin


---

## Functions/Methods

```rust
pub fn sum(first: i32, second: i32) -> i32 {
  first + second
}
```

```rust
fn main() {
  let calculation = sum(1, 2);
  assert_eq!(calculation, 3);
}
```

----

```rust
fn make_sound(dog: &Dog) -> String {
  dog.bark()
}
```

```rust
fn pet(dog: &mut Dog) {
  dog.set_happy();
}
```

----

```rust
let items: Vec<i32> = vec[6, 4, 2, 4];
let filtered_items: Vec<&i32> = items
  .iter()
  .filter(|it| *it > 4)
  .collect();

assert_eq(filtered_items, vec[&6]);
```

---

## Structs

```rust
pub struct Dog {
  is_happy: bool
}

impl Dog {
  pub fn new() -> Dog {
    Dog { is_happy: false }
  }
  pub fn bark(&self) -> String {
    "Woof".to_string()
  }
  pub fn set_happy(&mut self) {
    self.is_happy = true;
  }
}

----

```rust
let dog = Dog::new()
dog.bark();
```

```rust
let mut dog = Dog::new()
dog.set_happy(); // <-- mutates dog
```

---

## Traits

```rust
pub trait MakeSound {
  fn make_sound(&self) -> String;
}

impl MakeSound for Dog {
  fn make_sound(&self) -> String {
    self.bark()
  }
}
```

```rust
impl MakeSound for Cat {
  fn make_sound(&self) -> String {
    self.miauw()
  }
}
```

----

Static Polymorphism
```rust
struct Record(String);
pub fn record_sound<T: MakeSound>(sound_maker: &T) -> Record {
  Record(sound_maker.make_sound().clone())
}
```

Dynamic Polymorphism
```rust
let sound_makers: Vec<Box<dyn MakeSound>> = 
        vec[Box::new(Dog::new()), Box::new(Cat::new())];
```