# Changelog

All notable changes to the Aimi Programming Language will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial project structure
- Lexer with support for keywords, operators, literals
- Parser with AST for functions, structs, enums, traits
- LLVM IR code generation backend
- Cross-compilation targets (x86_64, ARM64, RISC-V, WebAssembly)
- Standard library modules (core, collections, io, memory, concurrency, ffi)
- CLI with build, run, check, tokens, ast commands
- Example programs (hello, calculator, fibonacci, advanced)
- Comprehensive documentation
- CI/CD pipeline for Linux, Windows, macOS
- Benchmark suite with multi-language comparison

### Changed
- N/A

### Deprecated
- N/A

### Removed
- N/A

### Fixed
- N/A

### Security
- N/A

## [0.1.0] - 2026-10-20

### Added
- Initial release of Aimi programming language
- Python-based LLVM compiler
- Syntax inspired by example format with colon-based declarations
- Memory safety with ownership and borrowing
- Generics and parametric polymorphism
- Pattern matching and algebraic data types
- Async/await concurrency model
- Metaprogramming with compile-time execution
- Foreign function interface for C interop
- Module system with package management
- Zero-cost abstractions
- Advanced optimizer with LLVM backend
- Standard library with collections, IO, memory, concurrency, FFI
- Cross-platform compilation to native machine code
- Comprehensive documentation and examples
- Full test suite and benchmark infrastructure

---

## Release Template

### [X.Y.Z] - YYYY-MM-DD

#### Added
- New features

#### Changed
- Changes in existing functionality

#### Deprecated
- Soon-to-be removed features

#### Removed
- Removed features

#### Fixed
- Bug fixes

#### Security
- Security fixes