<div align="center">

```text
███████╗████████╗███████╗██╗     ██╗      █████╗ ██████╗       ██████╗  █████╗ ████████╗██╗  ██╗
██╔════╝╚══██╔══╝██╔════╝██║     ██║     ██╔══██╗██╔══██╗      ██╔══██╗██╔══██╗╚══██╔══╝██║  ██║
███████╗   ██║   █████╗  ██║     ██║     ███████║██████╔╝█████╗██████╔╝███████║   ██║   ███████║
╚════██║   ██║   ██╔══╝  ██║     ██║     ██╔══██║██╔══██╗╚════╝██╔═══╝ ██╔══██║   ██║   ██╔══██║
███████║   ██║   ███████╗███████╗███████╗██║  ██║██║  ██║      ██║     ██║  ██║   ██║   ██║  ██║
╚══════╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝      ╚═╝     ╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝
```

### Deterministic Static Analysis, Security Linting & Developer Tooling for Soroban

[![Stellar Ecosystem](https://img.shields.io/badge/Stellar-Soroban-7B3FE4?style=for-the-badge&logo=stellar)](https://stellar.org)
[![Rust 2021](https://img.shields.io/badge/Rust-2021-DEA584?style=for-the-badge&logo=rust)](https://www.rust-lang.org)
[![Go 1.22+](https://img.shields.io/badge/Go-1.22+-00ADD8?style=for-the-badge&logo=go)](https://golang.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

<br/>

<p align="center">
  <b>STELLAR-PATH</b> is an end-to-end repository intelligence and security analysis framework designed to inspect Soroban smart contracts statically without requiring runtime WASM execution environments.
</p>

</div>

---

## 🔭 The STELLAR-PATH Toolchain Topology

```text
       +-------------------------------------------------------------+
       |                     Contract Developer                      |
       +------------------------------+------------------------------+
                                      |
                     1. Generate Scaffold Workspace
                                      v
       +-------------------------------------------------------------+
       |                  stellar-scaffold (Go CLI)                  |
       |  * Standardized directory trees                             |
       |  * Soroban SDK dependency pinning                           |
       |  * Automated test harness boilerplate                       |
       +------------------------------+------------------------------+
                                      |
                     2. Pre-Compile Static Inspection
                                      v
       +-------------------------------------------------------------+
       |                  stellarpath-cli (Rust Engine)              |
       |  * Abstract Syntax Tree (AST) Traversal (`syn`)             |
       |  * Typed DataKey collision prevention                       |
       |  * Instance / Persistent Storage TTL lifecycle checks       |
       |  * Modern RPC vs Horizon endpoint detection                 |
       |  * Security Mistakes (#17 panic, #18 unwrap, #19 events)   |
       +------------------------------+------------------------------+
                                      |
                     3. Continuous Integration Gatekeeper
                                      v
       +-------------------------------------------------------------+
       |               stellarpath-action (GitHub Action)            |
       |  * Pull Request AST auditing & automated review comments    |
       |  * Zero-warning verification rules                          |
       |  * SARIF / JSON diagnostic reporting                        |
       +-------------------------------------------------------------+
```

---

## 🔒 Example: Catching DataKey Collisions

Our deterministic static analysis enforces safe storage patterns automatically, preventing dangerous raw symbol collisions in smart contracts.

```rust
// ✅ SECURE: Typed variant prevents collision
#[contracttype]
#[derive(Clone)]
pub enum DataKey {
    Admin,
    Allowance(Address),
}

env.storage().instance().set(&DataKey::Admin, &admin);
env.storage().instance().extend_ttl(100, 1000);
```

---

## 📦 Active Ecosystem Repositories

| Repository | Tech Stack | Responsibility | Status |
| :--- | :--- | :--- | :--- |
| [**`stellarpath-cli`**](https://github.com/STELLAR-PATH/stellarpath-cli) | `Rust` `syn` `clap` | High-performance AST static analyzer inspecting Soroban contracts for security anti-patterns, storage collisions, and RPC hygiene using integer basis-points math. | `v0.1.0 (Wave Ready)` |
| [**`stellar-scaffold`**](https://github.com/STELLAR-PATH/stellar-scaffold) | `Go` `cli` | CLI scaffolding engine standardizing Soroban contract layout, unit test suites, and ecosystem configuration boilerplate. | `Active` |
| [**`stellarpath-action`**](https://github.com/STELLAR-PATH/stellarpath-action) | `TypeScript` `actions` | Automated GitHub Action executing deterministic lint checks directly inside pull requests to prevent regressions before mainnet deployment. | `Active` |

---

## ⚡ Quickstart

### 1. Static Contract Analysis (`stellarpath-cli`)

```bash
# Clone and build the deterministic engine
git clone https://github.com/STELLAR-PATH/stellarpath-cli.git
cd stellarpath-cli
cargo build --release

# Run static inspection across contract source files
./target/release/stellarpath scan ./contracts --format terminal
```

### 2. Scaffold a New Soroban Workspace (`stellar-scaffold`)

```bash
# Run the Go scaffolding generator
git clone https://github.com/STELLAR-PATH/stellar-scaffold.git
cd stellar-scaffold
go run main.go init my-soroban-project
```
