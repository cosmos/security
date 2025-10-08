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

A **Release Family** is defined as a specific combination of component versions. Support is limited to two families at any given time:

### Current Family 1 *(older, maintained until next family transition)*

- CometBFT **v0.38.x**
- Cosmos SDK **v0.50.x**
- IBC **v8.x**

### Current Family 2 *(newer, active)*

- CometBFT **v0.38.x**
- Cosmos SDK **v0.53.x**
- IBC **v10.x**
- Cosmos EVM **v0.5.x**

---

## Future Family Evolution

When a new family is introduced, the oldest family is retired. This ensures focus on stability, predictable upgrades, and reduces ecosystem fragmentation.

### Planned Future Family

- CometBFT **v0.39.x**
- Cosmos SDK **v0.54.x**
- IBC **v11.x**
- Cosmos EVM **v0.6.x**

Upon introduction of this family, support for the older *(0.50.x / IBC v8.x)* family will end.

---

## What Is Supported

- **Bug Fixes:** Critical security and stability issues are patched for all active families.
- **Compatibility:** All components within a family are guaranteed to work together.
- **Retirement:** Families are retired upon the introduction of a newer family. Retired families no longer receive patches or compatibility updates.
- **Upgradability:** We guarantee an upgrade path from one release family to the next adjacent family in the form of clear guides, compatibility and tooling for assistance.

---

## Security Fix Process

Cosmos Labs operates a bug bounty program on [HackerOne](https://www.hackerone.com/). We encourage responsible disclosure of vulnerabilities within the supported release families.

For bugs in working branches or in future releases, we encourage developers to share as early and often as possible so we can build a safer, more secure Stack.

The security fix process is being refined to provide better and more predictable service to developers and users. Changes are being introduced to improve transparency and response times across different issue severities:

- **Low and Medium severity:** Fixes will be developed publicly and included in a scheduled Patch Day release.
- **High severity:** Fixes will be developed privately and included in a scheduled Patch Day release.
- **Critical severity (e.g., fund loss):** Fixes will be developed privately and deployed immediately, outside the Patch Day cycle.

---

## Patch Day

**Patch Day** is a scheduled release event for security and stability fixes.

- Occurs on the **second Tuesday of each month**.
- A **5-day advance notice** will be provided detailing the packages affected and the nature of the fixes.

This ensures stakeholders can prepare, test, and deploy updates in a timely manner.
