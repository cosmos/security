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

Each release family is maintained for **one (1) year from the date it is introduced**.

As a general policy, Cosmos Labs intends to introduce **two release families per year**, which typically results in two active families at any given time. However, because each family is supported for one full year, there may be temporary periods where more than two families are active simultaneously.

In the event that a new release family is not introduced on schedule, the support window for the most recent family will extend beyond one year until a successor family is formally released. We will not allow a gap in supported release families.

### Current Family 1 *(older, maintained under 1-year lifecycle policy)*

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

When a new family is introduced, it begins its own one-year maintenance window.

Because families are supported for one year from release, the retirement of an older family is determined by its lifecycle timeline rather than strictly by the introduction of a new family. In practice, given our target cadence of two families per year, this will typically result in two active families at a time.

### Planned Future Family

- CometBFT **v0.39.x**
- Cosmos SDK **v0.54.x**
- IBC **v11.x**
- Cosmos EVM **v0.6.x**

Upon introduction of this family, it will enter its one-year maintenance window. The retirement date of older families will be determined based on their original release date and lifecycle timeline.

---

## What Is Supported

- **Bug Fixes:** Critical security and stability issues are patched for all active families.
- **Compatibility:** All components within a family are guaranteed to work together.
- **Lifecycle:** Each family is supported for one year from release, subject to extension if a successor family has not yet been introduced.
- **Retirement:** Once a family reaches the end of its lifecycle, it no longer receives patches or compatibility updates.
- **Upgradability:** We guarantee an upgrade path from one release family to the next adjacent family in the form of clear guides, compatibility guarantees, and tooling for assistance.

---

## Security Fix Process

Please read our [security policy](./SECURITY.md) for a detailed breakdown of how bugs and vulnerabilities are to be handled for the Cosmos Stack.

---

## Addendum: End of Life (EOL) Notices

The following releases were not covered under this Release Family policy, as it was not yet in place at the time of their lifecycle. However, they have had sufficient maintenance windows and will formally reach **End of Life (EOL) at the end of Q1 2026** with the release of our new Release Family:

- **CometBFT v0.37.x and lower**
- **ibc-go v0.7.x and lower**
- **Cosmos SDK v0.50.x and lower**

After the end of Q1 2026, these versions will no longer receive maintenance, security patches, or support from Cosmos Labs.

Additionally:

- **CometBFT v1.x** will not be supported. That release has been fully retracted and is not part of any supported release family.

We strongly encourage all teams running affected versions to plan their upgrades accordingly.
