# Dytallix

**The first solo-built PQC-native Layer 1 blockchain.**

Dytallix implements NIST-standardized PQC primitives at every layer of the protocol. ML-DSA-65 for all transaction signing and validator votes. ML-KEM-768 for all P2P transport. Canonical Bech32m addresses. No ECDSA. No hybrid mode. No legacy accounts. Every address, every signature, every handshake is quantum-secure from inception.

Designed, built, and deployed by one person in nine months. Testnet is live.

---

## Why This Exists

Adversaries are capturing encrypted traffic today to decrypt it once a cryptographically relevant quantum computer arrives — the "Harvest Now, Decrypt Later" threat is not future risk, it is present risk. Any blockchain that still accepts ECDSA signatures is accumulating cryptographic debt that a CRQC will collect on.

Dytallix is built so you never have to migrate.

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

   Create a wallet, print the D-Addr, and request DGT and DRT from the faucet:

   ```bash
   cargo install --git https://github.com/DytallixHQ/dytallix-sdk dytallix-cli --bin dytallix
   dytallix init
   ```

   Continue with: [first-transaction example](https://github.com/DytallixHQ/dytallix-sdk/blob/main/examples/first-transaction.rs) · [Explorer](https://dytallix.com/build/blockchain) · [Releases](https://github.com/DytallixHQ/dytallix-sdk/releases)

3. **First contract: under 15 minutes**

   Deploy a WASM contract from the CLI and move to contract iteration fast.

   Continue with: [deploy-contract example](https://github.com/DytallixHQ/dytallix-sdk/blob/main/examples/deploy-contract.rs) · [dytallix-contracts](https://github.com/DytallixHQ/dytallix-contracts) · [Docs](https://dytallix.com/docs)

→ [SDK repo](https://github.com/DytallixHQ/dytallix-sdk) · [Releases](https://github.com/DytallixHQ/dytallix-sdk/releases) · [Full getting started guide](https://dytallix.com/docs)

---

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk) | Official SDK and CLI. ML-DSA-65 keypairs, Bech32m addresses, transaction building, and the `dytallix` CLI with three developer milestones | Active |
| [dytallix-node](https://github.com/DytallixHQ/dytallix-node) | Public node, RPC, and backend source for the live testnet. Transaction submission, gas accounting, mempool, execution, and PQC verification | Live |
| [dytallix-faucet](https://github.com/DytallixHQ/dytallix-faucet) | Public faucet service repository documenting the live `dytallix.com/api/faucet` endpoints and request flow | Testnet |
| [dytallix-explorer](https://github.com/DytallixHQ/dytallix-explorer) | Public explorer service repository documenting the live `dytallix.com/build/blockchain` page and blockchain API surface | Testnet |
| [dytallix-docs](https://github.com/DytallixHQ/dytallix-docs) | Official documentation — getting started, CLI reference, SDK reference, core concepts, and FAQ | In progress |
| [dytallix-contracts](https://github.com/DytallixHQ/dytallix-contracts) | On-chain WASM protocol contracts — emission controller, DGT, DRT, staking, governance, and algorithm registry | In progress |

---

Canonical public integration guidance lives in
[dytallix-docs](https://github.com/DytallixHQ/dytallix-docs). The explorer and
faucet repositories document the live public service surfaces; they are not the
deployed frontend or backend source trees for those hosted services.

---

## The Cryptographic Stack

| Primitive | Standard | Use |
|-----------|----------|-----|
| ML-DSA-65 | FIPS 204 / Dilithium3 | All transaction signing and validator votes |
| ML-KEM-768 | FIPS 203 / Kyber768 | All P2P transport and handshakes |
| SLH-DSA-SHAKE-192s | FIPS 205 / SPHINCS+ | Optional cold storage signing |
| BLAKE3 | — | State hashing and address derivation |
| Bech32m | BIP350 | Address encoding with checksum |

All parameter sizes are exact. ML-DSA-65 public key is 1,952 bytes. Signature is 3,309 bytes. A single mistyped character in any address fails checksum validation. There is no classical fallback.

---

## Open Problems

We publish the parts of this protocol we are not fully satisfied with. A project that knows its own edges is more trustworthy than one that claims to have none.

- **VRF construction** — the current leader election uses a deterministic-signature-derived VRF that has not been formally proven to satisfy full VRF security properties. It is a practical stand-in pending a standardized PQC VRF.
- **Isochronous rejection sampling** — ML-DSA signing uses a variable-iteration rejection sampling loop. The implementation is designed to be constant-time but a formal side-channel analysis has not been completed.
- **Signature aggregation** — ML-DSA does not support constant-size non-interactive aggregation like BLS. Checkpoint finality uses Bitfield-Compressed Merkle Proofs instead. If efficient PQC aggregation is standardized we will adopt it.
- **Handshake formal verification** — the Noise_IK_PQC handshake has not been formally analyzed with ProVerif or Tamarin. Scheduled for pre-mainnet audit.

Full technical detail in the [Technical Whitepaper](https://dytallix.com/whitepaper).

---

## Whitepapers

Three documents covering different depths of the protocol:

- [Foundational Whitepaper](https://dytallix.com/whitepaper) — purpose, principles, architecture overview, business case, and roadmap
- [Technical Whitepaper](https://dytallix.com/whitepaper) — cryptographic specification, consensus formalization, networking, execution layer, and security analysis
- [Tokenomics Whitepaper](https://dytallix.com/whitepaper) — dual token model, PID emission controller, dimensional fee market, and governance

---

## Contributing

Dytallix was built by one person. The transition to a quantum-secure web requires more than one person.

We are looking for cryptographers to audit the PQC implementation, systems engineers to stress-test the testnet, and developers to build the first PQC-native dApps.

Start here: [dytallix-sdk](https://github.com/DytallixHQ/dytallix-sdk)

If you find something broken or something that could be better, open an issue. If you want to talk first, join Discord.

---

## Links

[Website](https://dytallix.com) · [Documentation](https://dytallix.com/docs) · [Whitepapers](https://dytallix.com/whitepaper) · [Discord](https://discord.gg/eyVvu5kmPG) · [Explorer](https://dytallix.com/build/blockchain) · [Faucet](https://dytallix.com/api/faucet/status) · [X](https://x.com/dytallixhq)

---

*Testnet is live. Mainnet is on the roadmap. Core protocol and developer tooling are open source; the public explorer and faucet repositories document the live service surfaces.*
