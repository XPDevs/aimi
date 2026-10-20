# Aimi Programming Language

Welcome to the Aimi Programming Language documentation. Aimi is a modern systems programming language with a Python-based LLVM compiler, designed to exceed C capabilities while maintaining familiar syntax patterns.

## Features

- **Cross-platform compilation** - Compiles to LLVM IR for native machine code on x86_64, ARM64, RISC-V, WebAssembly
- **Memory safety** - Ownership, borrowing, and lifetimes without garbage collection
- **Modern type system** - Generics, algebraic data types, traits, pattern matching
- **Concurrency** - Async/await, channels, threads, atomic operations
- **Metaprogramming** - Compile-time execution, macros, reflection
- **C interop** - Seamless FFI with zero-overhead bindings
- **Zero-cost abstractions** - High-level features compile to efficient machine code
- **Package manager** - Built-in dependency management and module system

## Quick Start

### Installation

```bash
pip install aimi
```

Or build from source:

```bash
git clone https://github.com/xpdevs/aimi
cd aimi
pip install -e .
```

### Hello World

Create a file `hello.aimi`:

```aimi
function: main {
    print: ("Hello World");
    exit();
}
```

Compile and run:

```bash
aimi hello.aimi -o hello
./hello
```

## Language Overview

### Syntax Style

Aimi uses a colon-based syntax inspired by the example format:

```aimi
function: name(parameters) {
    // statements
}

let: variable = value;
const: CONSTANT = value;

if: { condition } {
    // then branch
} else: {
    // else branch
}

match: expression {
    case: pattern => { body }
    case: pattern => { body }
}
```

### Basic Types

| Type | Description |
|------|-------------|
| `i8`, `i16`, `i32`, `i64` | Signed integers |
| `u8`, `u16`, `u32`, `u64` | Unsigned integers |
| `f32`, `f64` | Floating point |
| `bool` | Boolean |
| `char` | Unicode character |
| `string` | UTF-8 string |
| `void` | No value |

### Variables

```aimi
let: x = 42;           // immutable
let: mut y = 10;       // mutable
let: ref z = &x;       // immutable reference
let: mut ref w = &mut y; // mutable reference
const: PI = 3.14159;   // compile-time constant
```

### Functions

```aimi
function: add(a: i32, b: i32) -> i32 {
    return: a + b;
}

function: greet(name: string) {
    print: ("Hello, %s!" name);
}

function: main {
    let: result = add(10, 20);
    greet("World");
    exit();
}
```

### Control Flow

```aimi
// If-else
if: { x > 0 } {
    print: ("positive");
} else: {
    print: ("non-positive");
}

// Match expression
match: value {
    case: 0 => { print: ("zero"); }
    case: 1 => { print: ("one"); }
    case: n => { print: ("other: %n" n); }
}

// Loops
while: { condition } {
    // body
}

for: item in collection {
    // body
}

loop: {
    // infinite loop
    break; // or continue
}

// Goto/Checkpoint (from example style)
goto: 'label';
checkpoint: label;
```

### Structs and Enums

```aimi
struct: Point {
    x: f64;
    y: f64;
}

enum: Option<T> {
    Some { value: T };
    None;
}

impl: Point {
    function: new(x: f64, y: f64) -> Point {
        return: Point { x: x, y: y };
    }
    
    function: distance(self: Point, other: Point) -> f64 {
        let: dx = self.x - other.x;
        let: dy = self.y - other.y;
        return: (dx * dx + dy * dy).sqrt();
    }
}
```

### Traits (Interfaces)

```aimi
trait: Drawable {
    function: draw(self: Self) -> void;
    function: area(self: Self) -> f64;
}

impl: Drawable for Circle {
    function: draw(self: Circle) -> void {
        print: ("Drawing circle radius %f" self.radius);
    }
    
    function: area(self: Circle) -> f64 {
        return: 3.14159 * self.radius * self.radius;
    }
}
```

### Generics

```aimi
function: identity<T>(value: T) -> T {
    return: value;
}

struct: Pair<T, U> {
    first: T;
    second: U;
}

function: process<T: Drawable>(items: Vector<T>) {
    for: item in items {
        item.draw();
    }
}
```

### Concurrency

```aimi
use: concurrency::{Thread, Channel, Mutex, spawn};

function: worker(id: i32, ch: Channel<String>) {
    for: i in 0..5 {
        ch.send("Worker ".push(id.to_string()).push(": ").push(i.to_string()));
    }
}

function: main {
    let: ch = Channel::new(10);
    
    for: i in 0..3 {
        let: c = ch.clone();
        spawn: || { worker(i, c); };
    }
    
    for: _ in 0..15 {
        match: ch.try_recv() {
            case: Some(msg) => { print: ("%s" msg); }
            case: None => { Thread::yield_now(); }
        }
    }
    exit();
}
```

### Async/Await

```aimi
async function: fetch(url: String) -> Result<String, String> {
    let: response = await: http_get(url);
    return: response;
}

function: main {
    let: fut = fetch("https://api.example.com/data");
    let: result = await: fut;
    match: result {
        case: Ok(data) => { print: ("Got: %s" data); }
        case: Err(e) => { print: ("Error: %s" e); }
    }
    exit();
}
```

### Memory Management

```aimi
use: memory::{Box, Rc, Arc, UniquePtr};

function: main {
    // Owned heap allocation
    let: boxed = Box::new(42);
    print: ("Boxed: %n" boxed.unwrap());
    
    // Reference counted
    let: rc = Rc::new(String::from("shared"));
    let: rc2 = rc.clone();
    
    // Atomic reference counted (thread-safe)
    let: arc = Arc::new(Mutex::new(0));
    let: arc2 = arc.clone();
    
    spawn: || {
        let: mut g = arc.lock();
        *g = *g + 1;
    };
    
    exit();
}
```

### FFI (C Interop)

```aimi
use: ffi::{CLibrary, CType, CString};

function: main {
    let: libc = CLibrary::load("c");
    let: puts = libc.get_function("puts", [CType.STRING], CType.INT);
    
    let: msg = CString::new("Hello from C!");
    puts.call(msg.as_ptr());
    
    exit();
}
```

## Standard Library

### Core Modules

- `core` - Basic functions (print, exit, memory, math)
- `collections` - Vector, HashMap, LinkedList, String, Option, Result
- `io` - File, Stdin, Stdout, Stderr, filesystem operations
- `memory` - Box, Rc, Arc, UniquePtr, allocators, layouts
- `concurrency` - Thread, Mutex, RwLock, Channel, async runtime
- `ffi` - CLibrary, CStruct, CFunction, callbacks

### Example Usage

```aimi
import: "collections" -> { Vector, HashMap, String };
import: "io" -> { File, read_to_string };

function: main {
    let: vec = Vector::new();
    vec.push(1);
    vec.push(2);
    vec.push(3);
    
    let: map = HashMap::new();
    map.insert("key", "value");
    
    let: content = read_to_string("file.txt");
    print: ("File: %s" content);
    
    exit();
}
```

## Compiler Usage

### Command Line

```bash
# Compile to executable
aimi build source.aimi -o output

# Compile to LLVM IR
aimi build source.aimi --emit llvm-ir -o output.ll

# Compile to assembly
aimi build source.aimi --emit asm -o output.s

# Compile to object file
aimi build source.aimi --emit obj -o output.o

# Run directly
aimi run source.aimi

# Check syntax only
aimi check source.aimi

# Show tokens
aimi tokens source.aimi

# Show AST
aimi ast source.aimi

# List targets
aimi targets
```

### Options

| Option | Description |
|--------|-------------|
| `-o, --output` | Output file path |
| `--target` | Target triple (default: host) |
| `-O` | Optimization level 0-3 (default: 2) |
| `--emit` | Output format: obj, asm, llvm-ir, exe |
| `--no-stdlib` | Don't link standard library |
| `-v, --verbose` | Verbose output |

### Target Triples

| Target | Description |
|--------|-------------|
| `host` | Host platform (default) |
| `x86_64-linux-gnu` | Linux x86_64 (glibc) |
| `x86_64-linux-musl` | Linux x86_64 (musl) |
| `x86_64-windows-msvc` | Windows x86_64 (MSVC) |
| `x86_64-windows-gnu` | Windows x86_64 (MinGW) |
| `aarch64-linux-gnu` | Linux ARM64 |
| `aarch64-macos` | macOS ARM64 |
| `wasm32-wasi` | WebAssembly WASI |
| `riscv64-linux-gnu` | Linux RISC-V 64 |

## Project Structure

```
aimi/
├── src/
│   └── aimi/
│       ├── lexer/      # Tokenizer
│       ├── parser/     # Parser & AST
│       ├── codegen/    # LLVM IR generation
│       ├── optimizer/  # Optimization passes
│       ├── target/     # Cross-compilation targets
│       ├── stdlib/     # Standard library
│       ├── cli.py      # Command line interface
│       ├── compiler.py # Compiler pipeline
│       └── build.py    # Build utilities
├── tests/              # Test suite
├── examples/           # Example programs
├── docs/               # Documentation
├── benchmarks/         # Performance benchmarks
├── .github/workflows/  # CI/CD
├── pyproject.toml      # Package config
└── README.md
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests: `pytest tests -v`
5. Run linters: `ruff check src tests && mypy src`
6. Submit a pull request

## License

MIT License - see LICENSE file for details.

## Support

- GitHub Issues: [github.com/xpdevs/aimi/issues](https://github.com/xpdevs/aimi/issues)
- Discussions: [github.com/xpdevs/aimi/discussions](https://github.com/xpdevs/aimi/discussions)

---

Built by XPDevs