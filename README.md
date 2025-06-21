# Roadmap: Rust Native Monero Wallet RPC

## Phase 0: Research & Foundation (Week 1)
-   **Objective:** Analyze Monero protocols and finalize the Rust technology stack.
-   **Key Deliverables:**
    -   Complete review of Monero wallet/daemon RPC specifications.
    -   Finalize choice of core crates (`tokio`, `axum`, `serde`, `reqwest`, `thiserror`).
    -   Produce a high-level architectural design for core modules (`rpc_server`, `daemon_client`, `wallet_state`, `scanner`).

## Phase 1: Core RPC Server & Proxy Layer (Weeks 2-3)
-   **Objective:** Build a functional RPC server that proxies initial requests to a running Monero Wallet RPC.
-   **Key Deliverables:**
    -   A robust `daemon_client` module for communicating with `monerod`.
    -   An `axum`-based JSON-RPC server.
    -   Proxy implementations and/or rough read only implementstions for `get_balance`, `get_address`, `transfer`, and `get_transfers`.
    -   Basic file-based configuration and structured logging (`tracing`).
    -   Integration tests verifying full intended functionality against a  daemon.

## Phase 2: Native Read-Only Wallet & Scanning (Weeks 4-8)
-   **Objective:** Replace read-only proxying with a native Rust backend that manages keys and scans the blockchain.
-   **Key Deliverables:**
    -   Native key/address generation and secure in-memory management.
    -   Persistent wallet state using `sled` or more likely `rocksdb` for UTXOs and transaction history.
    -   A native blockchain `scanner` module that syncs with the daemon.
    -   RPC methods `get_balance`, `get_transfers`, and `get_address` now served conpletely natively.
    -   RPC server secured with authentication and optionsl SSL/TLS.

## Phase 3: Native Transaction Creation (Weeks 8-14)
-   **Objective:** Achieve full native functionality by implementing transaction creation, removing all dependencies on an external Monero wallet process.
-   **Key Deliverables:**
    -   Native UTXO selection and RingCT transaction construction logic.
    -   Native transaction signing using the wallet's private spend key.
    -   RPC methods `transfer` and `sweep_all` now fully native.
    -   The external Monero Wallet RPC is no longer required.
    -   End-to-end tests for creating a wallet, receiving, and sending funds natively on a testnet.

## Phase 4: Advanced Features & Production Readiness (Weeks 15+)
-   **Objective:** Harden the RPC for production use and add advanced features.
-   **Key Deliverables:**
    -   Implementation of multi-signature wallet support.
    -   Monitoring via a Prometheus metrics endpoint.
    -   Containerization (Dockerfile) and CI/CD pipeline for automated builds.
    -   Comprehensive API documentation and user guides.
    -   (Stretch Goal) Hardware wallet integration for signing.
