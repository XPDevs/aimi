# Aimi Package Manager Configuration

## aimi.toml

```toml
[package]
name = "my_project"
version = "0.1.0"
edition = "2026"
description = "A sample Aimi project"
authors = ["Your Name <you@example.com>"]
license = "MIT"
repository = "https://github.com/user/my_project"
homepage = "https://github.com/user/my_project"
documentation = "https://docs.rs/my_project"
keywords = ["example", "demo"]
categories = ["command-line-utilities"]

[dependencies]
collections = "1.0"
io = "1.0"
concurrency = "1.0"

[dev-dependencies]
test_utils = "0.1"

[features]
default = ["std"]
std = []
serde = ["collections/serde", "io/serde"]

[profile.release]
opt-level = 3
lto = true
codegen-units = 1
panic = "abort"

[profile.dev]
opt-level = 0
debug = true

[workspace]
members = ["crates/*"]
resolver = "2"

[target.x86_64-unknown-linux-gnu]
linker = "clang"

[target.aarch64-unknown-linux-gnu]
linker = "clang"

[build]
rustc-flags = ["-C", "target-cpu=native"]
```

## Package Registry

The Aimi package registry is hosted at `https://crates.aimi.dev`

### Publishing

```bash
# Login
aimi login

# Publish
aimi publish

# Publish specific version
aimi publish --version 1.0.0
```

### Dependency Resolution

Aimi uses a SAT solver for dependency resolution with the following features:
- Semantic versioning (SemVer)
- Feature unification
- Minimal version selection
- Lock file for reproducible builds

### Lock File

```toml
# aimi.lock
[[package]]
name = "collections"
version = "1.2.3"
source = "registry+https://crates.aimi.dev"
dependencies = [
  "memory 1.0",
]

[[package]]
name = "memory"
version = "1.0.0"
source = "registry+https://crates.aimi.dev"
```

## Workspaces

```toml
# Root aimi.toml
[workspace]
members = [
  "cli",
  "lib",
  "macros",
]
resolver = "2"

[workspace.dependencies]
collections = { version = "1.0", features = ["serde"] }
anyhow = "1.0"
```

## Overrides

```toml
[patch.crates-io]
collections = { path = "../collections-fork" }

[replace]
"collections:1.0" = { path = "../collections-local" }
```

## Configuration

```toml
# ~/.config/aimi/config.toml
[registry]
index = "https://github.com/aimi/registry-index"
token = "your-token-here"

[build]
jobs = 4
target-dir = "target"

[net]
proxy = "http://proxy.example.com:8080"
offline = false

[alias]
c = "check"
b = "build"
r = "run"
t = "test"
```