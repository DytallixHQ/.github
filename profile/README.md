# Dytallix

**The first solo-built PQC-native Layer 1 blockchain.**

Keypair, faucet, transfer, and basic contract lifecycle are available for experimentation on the public testnet. Staking, governance, and some advanced or operator paths are not yet production-complete.

Dytallix implements NIST-standardized PQC primitives at every layer of the protocol. ML-DSA-65 for all transaction signing and validator votes. ML-KEM-768 for all P2P transport. Canonical Bech32m addresses. No ECDSA. No hybrid mode. No legacy accounts. Every address, every signature, every handshake is quantum-secure from inception.

Designed, built, and deployed by one person in nine months. Testnet is live.

---

## Why This Exists

Adversaries are capturing encrypted traffic today to decrypt it once a cryptographically relevant quantum computer arrives — the "Harvest Now, Decrypt Later" threat is not future risk, it is present risk. Any blockchain that still accepts ECDSA signatures is accumulating cryptographic debt that a CRQC will collect on.

Dytallix is built so you never have to migrate.

---

### Prerequisites

- [Rust](https://www.rust-lang.org/tools/install) (stable toolchain) and Cargo.  
  Install via rustup (recommended):
  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

---

## Developer Path

These are the three developer milestones Dytallix is optimizing for:

1. **First keypair: under 60 seconds**

   Generate your first ML-DSA-65 keypair and print a D-Addr:

   ```bash
   git clone https://github.com/DytallixHQ/dytallix-sdk
   cd dytallix-sdk
   cargo run -p dytallix-sdk --example first-keypair
   ```

   Start here: [first-keypair example](https://github.com/DytallixHQ/dytallix-sdk/blob/main/examples/first-keypair.rs)

2. **First transaction on testnet: 2-3 minutes**

   Create a wallet, print the D-Addr, request DGT and DRT from the faucet, then
   submit a real transaction:

   ```bash
   cargo install --git https://github.com/DytallixHQ/dytallix-sdk.git dytallix-cli --bin dytallix
   dytallix init
   dytallix send <daddr> 100
   ```

   Use the D-Addr printed by `dytallix init` or any other testnet address.

   Continue with: [first-transaction example](https://github.com/DytallixHQ/dytallix-sdk/blob/main/examples/first-transaction.rs) · [Explorer](https://dytallix.com/build/blockchain) · [Releases](https://github.com/DytallixHQ/dytallix-sdk/releases)

3. **First contract build: under 15 minutes**

   Build a minimal WASM contract now. The default public gateway currently does
   not accept `POST /contracts/deploy`, so actual deploys require a direct node
   endpoint or a local node.

   ```bash
   rustup target add wasm32-unknown-unknown
   cargo build --manifest-path examples/contracts/minimal_contract/Cargo.toml --target wasm32-unknown-unknown --release
   ```

   Continue with: [deploy-contract example](https://github.com/DytallixHQ/dytallix-sdk/blob/main/examples/deploy-contract.rs) · [dytallix-contracts](https://github.com/DytallixHQ/dytallix-contracts) · [Docs](https://dytallix.com/docs)

→ [SDK repo](https://github.com/DytallixHQ/dytallix-sdk) · [Releases](https://github.com/DytallixHQ/dytallix-sdk/releases) · [Full getting started guide](https://dytallix.com/docs)

---

## Recommended Pinned Repositories

For broad developer outreach, pin these repositories on the organization page:

1. [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk) — primary entry point for keypair generation, first transaction, and SDK/CLI integration.
2. [dytallix-docs](https://github.com/DytallixHQ/dytallix-docs) — canonical developer documentation and reference material.
3. [dytallix-node](https://github.com/DytallixHQ/dytallix-node) — canonical public node and RPC backend source for testnet integration context.

---

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk) | Official SDK and CLI. ML-DSA-65 keypairs, Bech32m addresses, transaction building, and the `dytallix` CLI with three developer milestones | Active |
| [dytallix-pqc](https://github.com/DytallixHQ/dytallix-pqc) | Standalone post-quantum cryptography crate and CLI tools — ML-DSA, FN-DSA, SLH-DSA, ML-KEM, bridge signing, key generation, verification, performance benchmarks, and PQC evidence generation | Active |
| [dytallix-node](https://github.com/DytallixHQ/dytallix-node) | Public node, RPC, and backend source for the public testnet, with clean-checkout production provenance and a published machine-readable capability contract | Canonical public node source |
| [dytallix-faucet](https://github.com/DytallixHQ/dytallix-faucet) | Public faucet backend source for the live `dytallix.com/api/faucet` flow, including edge compatibility config | Canonical faucet backend source |
| [dytallix-explorer](https://github.com/DytallixHQ/dytallix-explorer) | Explorer service-surface documentation repo for the live `dytallix.com/build/blockchain` page and blockchain API surface | Docs-only surface map |
| [dytallix-docs](https://github.com/DytallixHQ/dytallix-docs) | Canonical public documentation for getting started, CLI reference, SDK reference, core concepts, and FAQ | Canonical docs |
| [dytallix-contracts](https://github.com/DytallixHQ/dytallix-contracts) | On-chain WASM protocol contracts — emission controller, DGT, DRT, staking, governance, and algorithm registry | In progress |

---

Canonical public integration guidance lives in
[dytallix-docs](https://github.com/DytallixHQ/dytallix-docs). The live website
frontend and hosted explorer UI remain public runtime surfaces at
[dytallix.com](https://dytallix.com), and the live faucet backend source is public in
[dytallix-faucet](https://github.com/DytallixHQ/dytallix-faucet).

The [dytallix-explorer](https://github.com/DytallixHQ/dytallix-explorer)
repository remains a docs-only surface map for the explorer endpoints. The node
repo now has clean-checkout production provenance from the public deployment.

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

Reference implementation and developer docs: [dytallix-pqc](https://github.com/DytallixHQ/dytallix-pqc) · [PQC docs](https://github.com/DytallixHQ/dytallix-pqc/tree/main/docs) · [CLI tools](https://github.com/DytallixHQ/dytallix-pqc/tree/main/src/bin)

---

## Open Problems

We publish the parts of this protocol we are not fully satisfied with. A project that knows its own edges is more trustworthy than one that claims to have none.

- **VRF construction** — the current leader election uses a deterministic-signature-derived VRF that has not been formally proven to satisfy full VRF security properties. It is a practical stand-in pending a standardized PQC VRF.
- **Isochronous rejection sampling** — ML-DSA signing uses a variable-iteration rejection sampling loop. The implementation is designed to be constant-time but a formal side-channel analysis has not been completed.
- **Signature aggregation** — ML-DSA does not support constant-size non-interactive aggregation like BLS. Checkpoint finality uses Bitfield-Compressed Merkle Proofs instead. If efficient PQC aggregation is standardized we will adopt it.
- **Handshake formal verification** — the Noise_IK_PQC handshake has not been formally analyzed with ProVerif or Tamarin. Scheduled for pre-mainnet audit.

Full technical detail and current long-form materials live at [Resources](https://dytallix.com/resources).

---

## Whitepapers

Long-form protocol papers and supporting materials are indexed on the main resources page:

- [Resources](https://dytallix.com/resources) — whitepapers, protocol background, and supporting materials

---

## Contributing

Dytallix was built by one person. The transition to a quantum-secure web requires more than one person.

We are looking for cryptographers to audit the PQC implementation, systems engineers to stress-test the testnet, and developers to build the first PQC-native dApps.

Start here: [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk)

If you find something broken or something that could be better, open an issue. If you want to talk first, join Discord.

---

## Links

[Website](https://dytallix.com) · [Documentation](https://dytallix.com/docs) · [Resources](https://dytallix.com/resources) · [Discord](https://discord.gg/eyVvu5kmPG) · [Explorer](https://dytallix.com/build/blockchain) · [Faucet](https://dytallix.com/api/faucet/status) · [X](https://x.com/dytallixhq)

---

*Testnet is live. Mainnet is on the roadmap. Core protocol and developer tooling are open source; the public explorer and faucet repositories document the live service surfaces.*
