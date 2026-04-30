# Release and Maintenance Policy for Core Stack Components

## Overview

This policy defines how Cosmos Labs manages maintenance and support for the core Cosmos Stack components:

- **CometBFT**
- **Cosmos SDK**
- **Cosmos EVM**
- **Inter-Blockchain Communication Protocol (IBC)**

This release process aims to provide clarity and predictability to both developers using the Stack and the Cosmos Labs engineering team. Developers should know exactly which software combinations are supported and should be used in production. At the same time, the Cosmos Labs team can coordinate fixes, security patches, and upgrades across a smaller set of well-defined release families, allowing for faster response times and more predictable maintenance.

To achieve this, we are introducing the concept of **Release Families**, curated sets of component versions of the Stack. Each family is fully tested for compatibility, stability, and long-term support. Maintenance and bug fixes are provided only for active families.

---

## Release Families

A **Release Family** is defined as a specific combination of component versions.

The canonical source of truth for release family lifecycle, active support windows, and retirement policy is maintained in Cosmos docs:

- [https://docs.cosmos.network/sdk/latest/release-family](https://docs.cosmos.network/sdk/latest/release-family)
- [https://github.com/cosmos/docs/blob/main/sdk/latest/release-family.mdx](https://github.com/cosmos/docs/blob/main/sdk/latest/release-family.mdx)

This file intentionally does not duplicate lifecycle timelines to avoid policy drift across multiple sources.

---

## What Is Supported

- **Bug Fixes:** Critical security and stability issues are patched for all active families.
- **Compatibility:** All components within a family are guaranteed to work together.
- **Lifecycle and Retirement:** Maintained on the canonical Release Families page in Cosmos docs.
- **Upgradability:** We guarantee an upgrade path from one release family to the next adjacent family in the form of clear guides, compatibility guarantees, and tooling for assistance.

---

## Security Fix Process

Please read our [security policy](./SECURITY.md) for a detailed breakdown of how bugs and vulnerabilities are to be handled for the Cosmos Stack.

---

## End of Life (EOL) Notices

Current and historical EOL notices for release families are maintained on the canonical Release Families page in Cosmos docs:

- [https://docs.cosmos.network/sdk/latest/release-family](https://docs.cosmos.network/sdk/latest/release-family)

CometBFT v1.x is not supported. That release line was retracted and is not part of any supported release family.
