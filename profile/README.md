# Dytallix

[![Website](https://img.shields.io/badge/website-dytallix.com-0f766e)](https://dytallix.com)
[![Docs](https://img.shields.io/badge/docs-live-2563eb)](https://dytallix.com/developers/docs)
[![Mainnet](https://img.shields.io/badge/mainnet-pre--launch%20simulations-d97706)](https://dytallix.com/developers/launch)
[![Testnet](https://img.shields.io/badge/testnet-retired-6b7280)](https://dytallix.com/developers/launch#testnet-retired)
[![PQC](https://img.shields.io/badge/PQC-ML--DSA--65%20%7C%20ML--KEM--768-7c3aed)](https://github.com/DytallixHQ/dytallix/tree/main/pqc)
[![GitHub](https://img.shields.io/badge/GitHub-DytallixHQ-111827)](https://github.com/DytallixHQ)

**A PQC-native Layer 1 blockchain.**

The public testnet was retired on 4 October 2026, together with its faucet, explorer, wallet and test assets. Dytallix is now running pre-mainnet launch simulations: seven pass/fail rehearsal runs (R01 to R07) and a statistical attack and fault campaign. They run on the production hosts, which serve as staging, and use rehearsal keys only. Mainnet has not launched, and no launch is authorized until every launch gate passes. Progress is published at [dytallix.com/developers/launch](https://dytallix.com/developers/launch).

Dytallix implements NIST-standardized PQC primitives at every layer of the protocol. ML-DSA-65 for all transaction signing and validator votes. ML-KEM-768 for all P2P transport. Canonical Bech32m addresses. No ECDSA. No hybrid mode. No legacy accounts. Every address, every signature, every handshake is quantum-secure from inception.

Dytallix is a small startup developing a post-quantum product ecosystem.

**Co-founders:** Andrew Holland and Rick Glenn. [About Dytallix](https://www.dytallix.com/company).

---

## Project Metadata

| Field | Value |
|-------|-------|
| Network | Pre-mainnet launch simulations (public testnet retired 4 October 2026) |
| Protocol category | PQC-native Layer 1 blockchain |
| Consensus | CometBFT v0.40.0 fork with PQC transport and a Rust ABCI application |
| Consensus signing | ML-DSA-65 |
| P2P transport | ML-KEM-768 |
| Address format | Canonical Bech32m D-Addr |
| Mainnet v1 scope | Ordinary, governance and recovery transactions; no contract runtime or cross-chain bridge |
| Source | [DytallixHQ/dytallix](https://github.com/DytallixHQ/dytallix): node, SDK and CLI, PQC primitives, docs, launch records, reproducible release |
| Organization | Small startup |
| Co-founders | Andrew Holland and Rick Glenn |

**Discovery tags:** `post-quantum-cryptography` · `pqc` · `quantum-safe` · `layer1` · `blockchain` · `mainnet` · `cometbft` · `ml-dsa` · `ml-kem` · `bech32m` · `rust` · `go` · `sdk` · `cli`

---

## Active Tasks

- [x] Publish the mainnet candidate as open source in [DytallixHQ/dytallix](https://github.com/DytallixHQ/dytallix), with a reproducible release build.
- [x] Document the NIST PQC baseline: ML-DSA-65 signing, ML-KEM-768 transport and Bech32m addresses.
- [x] Retire the public testnet and approve the pre-mainnet simulation plan and pass criteria.
- [ ] Pass the launch rehearsal runs R01 to R07 on the production hosts as staging.
- [ ] Pass the attack and fault campaign: transactions, staking, governance, root controls, recovery, endpoints, network, faults, performance and endurance.
- [ ] Complete the security assessment (underway) and the public review period.
- [ ] Formalize VRF construction, handshake analysis and side-channel review before mainnet.
- [ ] Pass all launch gates, then hold the genesis ceremony.

The simulation plan and pass criteria are in [P01_T06_SIMULATION_PLAN_2026-10-11.json](https://github.com/DytallixHQ/dytallix/blob/main/launch/approvals/P01_T06_SIMULATION_PLAN_2026-10-11.json) and [launch-rehearsals.md](https://github.com/DytallixHQ/dytallix/blob/main/node/docs/mainnet/launch-rehearsals.md). The launch gates are in [MAINNET_GATE_MASTER.md](https://github.com/DytallixHQ/dytallix/blob/main/launch/MAINNET_GATE_MASTER.md).

---

## Why This Exists

Adversaries are capturing encrypted traffic today to decrypt it once a cryptographically relevant quantum computer arrives — the "Harvest Now, Decrypt Later" threat is not future risk, it is present risk. Any blockchain that still accepts ECDSA signatures is accumulating cryptographic debt that a CRQC will collect on.

Dytallix is built so you never have to migrate.

---

## Prerequisites

Install [Rust](https://www.rust-lang.org/tools/install) with `rustup`. Each
workspace pins Rust 1.88.0 in its `rust-toolchain.toml`, so `rustup` fetches
the right toolchain on the first build. The consensus engine also needs
[Go](https://go.dev/dl/) 1.25.

---

## Developer Path

There is no public network to transact on while the simulations run: the
testnet and its faucet are retired, and mainnet has not launched. You can
still work with the code locally.

1. **First keypair: under 60 seconds**

   Generate an ML-DSA-65 keypair, derive a D-Addr, then sign and verify a
   message. The example runs offline:

   ```bash
   git clone https://github.com/DytallixHQ/dytallix
   cd dytallix/sdk
   cargo run -p dytallix-sdk --example first-keypair
   ```

   Start here: [first-keypair example](https://github.com/DytallixHQ/dytallix/blob/main/sdk/examples/first-keypair.rs)

2. **Build and test the node**

   From the repository root:

   ```bash
   cd node
   cargo build --workspace --all-targets --locked
   cargo test --workspace --locked
   ```

   The consensus engine lives in `node/consensus/cometbft`:

   ```bash
   cd node/consensus/cometbft
   go test -mod=readonly ./...
   ```

3. **Follow the launch simulations**

   Rehearsal and campaign results are published on the
   [launch dashboard](https://dytallix.com/developers/launch) as they come in.

→ [Mainnet repo](https://github.com/DytallixHQ/dytallix) · [Release build](https://github.com/DytallixHQ/dytallix/blob/main/release/README.md) · [Docs](https://dytallix.com/developers/docs)

---

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [dytallix](https://github.com/DytallixHQ/dytallix) | Mainnet candidate: consensus node, CometBFT fork with PQC transport, SDK and CLI, PQC primitives, docs, launch records and reproducible release | Canonical, active |
| [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk) | Testnet-era SDK and CLI | Superseded by [`dytallix/sdk`](https://github.com/DytallixHQ/dytallix/tree/main/sdk) |
| [dytallix-pqc](https://github.com/DytallixHQ/dytallix-pqc) | Standalone PQC crate and CLI tools — ML-DSA, FN-DSA, SLH-DSA, ML-KEM | Superseded by [`dytallix/pqc`](https://github.com/DytallixHQ/dytallix/tree/main/pqc) |
| [dytallix-node](https://github.com/DytallixHQ/dytallix-node) | Node, RPC and backend source for the retired public testnet | Testnet-era, superseded by [`dytallix/node`](https://github.com/DytallixHQ/dytallix/tree/main/node) |
| [dytallix-docs](https://github.com/DytallixHQ/dytallix-docs) | Testnet-era documentation | Superseded by [`dytallix/docs`](https://github.com/DytallixHQ/dytallix/tree/main/docs) |
| [dytallix-contracts](https://github.com/DytallixHQ/dytallix-contracts) | WASM reference contracts — emission controller, DGT, DRT, staking, governance, algorithm registry | Reference only; mainnet v1 has no contract runtime ([`dytallix/contracts`](https://github.com/DytallixHQ/dytallix/tree/main/contracts)) |
| [dytallix-faucet](https://github.com/DytallixHQ/dytallix-faucet) | Faucet backend for the retired testnet | Retired; mainnet has no faucet |
| [dytallix-explorer](https://github.com/DytallixHQ/dytallix-explorer) | Explorer surface map for the retired testnet | Retired |

All current work happens in [DytallixHQ/dytallix](https://github.com/DytallixHQ/dytallix).
The other repositories are kept for reference from the public testnet period.

---

## The Cryptographic Stack

| Primitive | Standard | Use |
|-----------|----------|-----|
| ML-DSA-65 | FIPS 204 | All transaction signing and validator votes |
| ML-KEM-768 | FIPS 203 | All P2P transport and handshakes |
| SLH-DSA-SHAKE-192s | FIPS 205 | Optional cold storage signing |
| BLAKE3 | — | State hashing and address derivation |
| Bech32m | BIP350 | Address encoding with checksum |

All parameter sizes are exact. ML-DSA-65 public key is 1,952 bytes. Signature is 3,309 bytes. A single mistyped character in any address fails checksum validation. There is no classical fallback.

Reference implementation: [`dytallix/pqc`](https://github.com/DytallixHQ/dytallix/tree/main/pqc) · [Trust model](https://github.com/DytallixHQ/dytallix/blob/main/launch/TRUST_MODEL.md)

---

## Open Problems

We publish the parts of this protocol we are not fully satisfied with. A project that knows its own edges is more trustworthy than one that claims to have none.

- **VRF construction** — the current leader election uses a deterministic-signature-derived VRF that has not been formally proven to satisfy full VRF security properties. It is a practical stand-in pending a standardized PQC VRF.
- **Isochronous rejection sampling** — ML-DSA signing uses a variable-iteration rejection sampling loop. The implementation is designed to be constant-time but a formal side-channel analysis has not been completed.
- **Signature aggregation** — ML-DSA does not support constant-size non-interactive aggregation like BLS. Checkpoint finality uses Bitfield-Compressed Merkle Proofs instead. If efficient PQC aggregation is standardized we will adopt it.
- **Handshake formal verification** — the Noise_IK_PQC handshake has not been formally analyzed with ProVerif or Tamarin. Scheduled for pre-mainnet audit.

Full technical detail and current long-form materials live at [Papers](https://dytallix.com/developers/papers).

---

## Whitepapers

Long-form protocol papers and supporting materials are indexed on the papers page:

- [Papers](https://dytallix.com/developers/papers) — whitepapers, protocol background, and supporting materials

---

## Contributing

We welcome contributors to the Dytallix protocol and developer tools.

We are looking for cryptographers to audit the PQC implementation, systems engineers to review the mainnet candidate and the launch simulation results, and developers to build the first PQC-native applications.

Start here: [DytallixHQ/dytallix](https://github.com/DytallixHQ/dytallix) · [CONTRIBUTING.md](https://github.com/DytallixHQ/dytallix/blob/main/CONTRIBUTING.md) (contributions are signed off under the DCO)

If you find something broken or something that could be better, open an issue. Report vulnerabilities privately through [SECURITY.md](https://github.com/DytallixHQ/dytallix/blob/main/SECURITY.md). If you want to talk first, join Discord.

---

## Links

[Website](https://dytallix.com) · [Launch simulations](https://dytallix.com/developers/launch) · [Documentation](https://dytallix.com/developers/docs) · [Papers](https://dytallix.com/developers/papers) · [Mainnet repo](https://github.com/DytallixHQ/dytallix) · [Discord](https://discord.gg/eyVvu5kmPG) · [X](https://x.com/dytallixhq)

---

*The public testnet is retired. Pre-mainnet launch simulations are underway, and mainnet launches only after every launch gate passes. All protocol code is open source in [DytallixHQ/dytallix](https://github.com/DytallixHQ/dytallix).*
