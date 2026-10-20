# Contributing to Aimi

Thank you for your interest in contributing to Aimi! This document provides guidelines for contributing to the project.

## Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct:
- Be respectful and inclusive
- Welcome newcomers and help them learn
- Focus on constructive criticism
- Accept feedback gracefully

## Getting Started

1. Fork the repository on GitHub
2. Clone your fork locally
3. Create a new branch for your feature/fix
4. Make your changes
5. Run tests and linters
6. Submit a pull request

## Development Setup

```bash
# Clone your fork
git clone https://github.com/yourusername/aimi.git
cd aimi

# Install development dependencies
pip install -r requirements.txt
pip install -e ".[dev]"

# Run tests to verify setup
pytest tests -v
```

## Project Structure

```
aimi/
├── src/aimi/          # Compiler source code
│   ├── lexer/         # Tokenizer
│   ├── parser/        # Parser & AST
│   ├── codegen/       # LLVM IR generation
│   ├── optimizer/     # Optimization passes
│   ├── target/        # Cross-compilation targets
│   ├── stdlib/        # Standard library
│   ├── cli.py         # Command line interface
│   ├── compiler.py    # Compiler pipeline
│   └── build.py       # Build utilities
├── tests/             # Test suite
├── examples/          # Example programs
├── docs/              # Documentation
├── benchmarks/        # Performance benchmarks
├── scripts/           # Build and release scripts
└── .github/workflows/ # CI/CD configuration
```

## Making Changes

### Code Style

- Follow PEP 8 for Python code
- Use type hints for all public functions
- Run `ruff format` before committing
- Run `ruff check` and `mypy` to catch issues

### Testing

- Add tests for new features in `tests/`
- Run `pytest tests -v` before submitting
- Aim for high test coverage

### Documentation

- Update documentation for user-facing changes
- Add docstrings to new public APIs
- Update `CHANGELOG.md` with your changes

## Pull Request Process

1. Ensure your branch is up to date with main
2. Run all checks: `./scripts/build.sh`
3. Fill out the PR template
4. Request review from maintainers
5. Address feedback and update PR
6. Once approved, maintainers will merge

## Commit Messages

Follow conventional commits format:

```
type(scope): description

[optional body]

[optional footer]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Test changes
- `chore`: Maintenance tasks

Examples:
```
feat(parser): add support for async/await syntax
fix(codegen): correct LLVM IR generation for structs
docs(stdlib): update Vector documentation
```

## Areas for Contribution

### Compiler
- LLVM IR optimization passes
- New target support (ARM, RISC-V, WebAssembly)
- Better error messages and diagnostics
- Incremental compilation

### Language Features
- Macro system
- Compile-time reflection
- More pattern matching features
- Generic associated types

### Standard Library
- More collection types
- Networking primitives
- Cryptography
- Serialization (JSON, TOML, etc.)

### Tooling
- Language server protocol (LSP) support
- VS Code extension
- Package manager improvements
- Debugger integration

### Documentation
- Tutorials and guides
- API documentation
- Migration guides
- Performance tips

## Reporting Issues

When reporting bugs, please include:
- Aimi version (`aimi --version`)
- Operating system and architecture
- Minimal reproduction case
- Expected vs actual behavior
- Error messages or stack traces

## Feature Requests

Feature requests should include:
- Clear description of the problem
- Proposed solution
- Use cases and examples
- Potential alternatives considered

## Security Issues

Report security vulnerabilities privately to security@xpdevs.example

## Recognition

Contributors will be recognized in:
- CONTRIBUTORS.md
- Release notes
- Project README

Thank you for contributing to Aimi!