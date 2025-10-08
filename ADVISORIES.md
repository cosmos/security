<p align="center">
<img src="./assets/advisories.png" alt="Advisories" width="500"/>
</p>

# Advisories

This is a list of all ASA advisories issued by the `/security` to date:

| Advisory                                                                                     | Team       | Severity | Title                                                                                                              |
| -------------------------------------------------------------------------------------------- | ---------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
|[ASA-2023-001](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-23px-mw2p-46qm) | Cosmos SDK | Medium|Cosmovisor|
|[ASA-2023-002](https://github.com/cometbft/cometbft/security/advisories/GHSA-hq58-p9mv-338c) | CometBFT | Low|Default for `BlockParams.MaxBytes` consensus parameter may increase block times and affect consensus participation|
|[ASA-2024-001](https://github.com/cometbft/cometbft/security/advisories/GHSA-qr8r-m495-7hc4) | CometBFT | High|Validation of `VoteExtensionsEnableHeight` can cause chain halt|
|[ASA-2024-002](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-2557-x9mg-76w8) | Cosmos SDK | Medium|Default `PrepareProposalHandler` may produce invalid proposals when used with default `SenderNonceMempool`|
|[ASA-2024-003](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-4j93-fm92-rp4m) | Cosmos SDK | Low|Missing `BlockedAddressed` Validation in Vesting Module|
|[ASA-2024-004](https://github.com/cometbft/cometbft/security/advisories/GHSA-555p-m4v6-cqxv) | CometBFT | Low|Default configuration param for Evidence may limit window of validity|
|[ASA-2024-005](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-86h5-xcpx-cfqc) | Cosmos SDK | Low|Potential slashing evasion during re-delegation|
|[ASA-2024-006](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-95rx-m9m5-m94v) | Cosmos SDK | High|ValidateVoteExtensions helper function may allow incorrect voting power assumptions|
|[ASA-2024-007](https://github.com/cosmos/ibc-go/security/advisories/GHSA-j496-crgh-34mx) | IBC-Go | Critical|Potential Reentrancy using Timeout Callbacks in ibc-hooks|
|[ASA-2024-008](https://github.com/cometbft/cometbft/security/advisories/GHSA-hg58-rf2h-6rr7) | CometBFT | Medium|Instability during blocksync when syncing from malicious peer|
|[ASA-2024-009](https://github.com/cometbft/cometbft/security/advisories/GHSA-g5xx-c4hv-9ccc) | CometBFT | Medium|State syncing validator from malicious node may lead to a chain split|
|[ASA-2024-010](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-7225-m954-23v7) | Cosmos SDK | High|cosmossdk.io/math: Mismatched bit-length validation in sdk.Int and sdk.Dec can lead to panic|
|[ASA-2024-011](https://github.com/cometbft/cometbft/security/advisories/GHSA-p7mv-53f2-4cwj) | CometBFT | High|Vote Extensions: Panic when receiving a Pre-commit with an invalid data|
|[ASA-2024-012](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-8wcc-m6j2-qxvm) | Cosmos SDK | High|ASA-2024-0012, ASA-2024-0013: CosmosSDK: Transaction decoding may result in a stack overflow or resource exhaustion|
|[ASA-2024-013](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-8wcc-m6j2-qxvm) | Cosmos SDK | High|ASA-2024-0012, ASA-2024-0013: CosmosSDK: Transaction decoding may result in a stack overflow or resource exhaustion|
|[ASA-2025-001](https://github.com/cometbft/cometbft/security/advisories/GHSA-22qq-3xwm-r5x4) | CometBFT | Medium|Malicious peer can disrupt node's ability to sync via blocksync|
|[ASA-2025-002](https://github.com/cometbft/cometbft/security/advisories/GHSA-r3r4-g7hq-pq4f) | CometBFT | High|Malicious peer can stall network by disseminating seemingly valid block parts|
|[ASA-2025-003](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-x5vx-95h7-rv4p) | Cosmos SDK | High|Group module can halt chain when handling a malicious proposal|
|[ASA-2025-004](https://github.com/cosmos/ibc-go/security/advisories/GHSA-jg6f-48ff-5xrw) | IBC-Go | Critical|Chain Halt via Non-deterministic deserialization|
