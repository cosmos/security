## Example Vulnerabilities for bug bounty
The following is a list of examples of the kinds of vulnerabilities that we’re
most interested in. It is not exhaustive: there are other kinds of issues we may
also be interested in!

### Specifications

* Conceptual flaws
* Ambiguities, inconsistencies, or incorrect statements
* Mismatch between specification and implementation of any component

### Consensus

Assuming less than 1/3 of the voting power is Byzantine (malicious):

* Validation of blockchain data structures, including blocks, block parts,
  votes, and so on
* Execution of blocks
* Validator set changes
* Proposer round-robin
* Two nodes committing conflicting blocks for the same height (safety failure)
* A correct node signing conflicting votes
* A node halting (liveness failure)
* Syncing new and old nodes

Assuming more than 1/3 the voting power is Byzantine:

* Attacks that go unpunished (unhandled evidence)

### Networking

* Replay attacks
* Eclipse attacks
* Sybil attacks
* Long-range attacks
* Denial-of-Service
* Network channel attacks

### RPC

* Write-access to anything besides sending transactions
* Leakage of secrets

Note: RPC DDoS resource exhaustion attacks are NOT in scope. Use operational best practices, proxies, etc.

### Denial-of-Service

Attacks may come through the P2P network:

* Amplification attacks
* Resource abuse
* Deadlocks and race conditions

### Libraries

* Serialization
* Reading/Writing files and databases

### Cryptography

* Elliptic curves for validator signatures
* Hash algorithms and Merkle trees for block validation
* Authenticated encryption for P2P connections

### Light Client

* Core verification
* Bisection/sequential algorithms

### Gaia

* Injection exploits
* Privilege escalation
* IBC
* Inter-module interactions

### How we process Tx parameters in the SDK

- Integer operations on tx parameters, especially `sdk.Int` / `sdk.Dec`
- Gas calculation & parameter choices
- Tx signature verification (see [`x/auth/ante`](https://github.com/cosmos/cosmos-sdk/tree/master/x/auth/ante))
- Possible Node DoS vectors (perhaps due to gas weighting / non constant timing)

### Handling private keys

- HD key derivation, local and Ledger, and all key-management functionality
- Side-channel attack vectors with our implementations
  - e.g. key exfiltration based on time or memory-access patterns when decrypting privkey
