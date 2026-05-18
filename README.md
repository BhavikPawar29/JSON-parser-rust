# JSON Parser in Rust

A lightweight JSON parser written in Rust using a custom lexer and recursive descent parser.  
This project demonstrates how JSON parsing works internally without relying on external parsing libraries.

---

# Features

- Parse JSON primitive values:
  - `null`
  - `true`
  - `false`
  - numbers
  - strings
- Parse JSON arrays
- Parse JSON objects
- Handle nested structures
- Unicode escape support (`\uXXXX`)
- Escape sequence handling:
  - `\n`
  - `\t`
  - `\\`
  - `\"`
- Pretty JSON output formatting

---

# Components

## Lexer

The lexer converts raw input text into a stream of tokens.

Example:

```json
{"name":"Alice"}
```

Becomes:

```text
LeftBrace
String("name")
Colon
String("Alice")
RightBrace
```

---

## Parser

The parser uses recursive descent parsing to transform tokens into structured JSON values.

Supported structures:

- Objects
- Arrays
- Strings
- Numbers
- Booleans
- Null

---

## JSONValue Enum

JSON data is represented using Rust enums.

Example:

```rust
enum JSONValue {
    Null,
    Bool(bool),
    Number(f64),
    String(String),
    Array(Vec<JSONValue>),
    Object(HashMap<String, JSONValue>),
}
```

---

# Supported JSON Examples

## Primitive Values

```json
null
true
false
123
-45.67
"hello world"
```

---

## Arrays

```json
[1, 2, 3, 4]
```

Nested arrays:

```json
[1, [2, 3], [4, [5]]]
```

---

## Objects

```json
{
  "name": "Alice",
  "age": 25,
  "active": true
}
```

---

## Nested Structures

```json
{
  "user": {
    "name": "Bob",
    "skills": ["Rust", "C++", "Python"]
  },
  "verified": false,
  "score": 99.5
}
```

---

# Running the Project

## Using Rust Compiler

Compile:

```bash
rustc main.rs
```

Run:

```bash
./main
```

---

## Using Cargo

Initialize cargo project:

```bash
cargo init
```

Run:

```bash
cargo run
```

---

# Example

## Input

```json
{
  "name": "Alice",
  "age": 25,
  "languages": ["Rust", "Python"]
}
```

## Output

```json
{
  "name": "Alice",
  "age": 25,
  "languages": [
    "Rust",
    "Python"
  ]
}
```

---

# How It Works

## Step 1 — Tokenization

The lexer scans characters one by one and converts them into tokens.

Example:

```text
{ "key": 10 }
```

Tokens:

```text
LeftBrace
String("key")
Colon
Number(10)
RightBrace
```

---

## Step 2 — Parsing

The parser recursively processes tokens.

Example flow:

```text
parse_object()
 ├── parse_string()
 ├── parse_number()
 └── parse_array()
```

---

# Example Test Cases

## Valid JSON

```json
{"a":1}
[1,2,3]
true
null
"hello"
```

## Invalid JSON

```json
{key:1}
[1,2,]
"unterminated
```

---

# Technologies Used

- Rust
- Standard Library only

No external crates are required.

# Author

Built for learning and understanding how JSON parsers work internally using Rust.