# Aimi Programming Language

A modern systems programming language with Python based LLVM compiler. Designed to exceed C capabilities while maintaining familiar syntax patterns. Built by XPDevs.

## Features

- Compiles to LLVM IR for cross platform machine code generation
- Memory safety with ownership and borrowing
- Generics and parametric polymorphism
- Pattern matching and algebraic data types
- Async await concurrency model
- Metaprogramming with compile time execution
- Foreign function interface for C interop
- Module system with package management
- Zero cost abstractions
- Advanced optimizer with LLVM backend

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Build the compiler
python -m aimi.build

# Compile a program
python -m aimi examples/hello.aimi -o hello

# Run the program
./hello
```

## Example

```aimi
function: main {
    print: ("Hello World");
    exit();
}
```

## Documentation

See docs/ for complete language reference and compiler internals.

## License

MIT License. See LICENSE file.