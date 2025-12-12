# Cosmos Security Vulnerability Disclosure and Bug Bounty Policy

## Introduction

Cosmos Labs is committed to the security of the Cosmos Stack and
encourages responsible disclosure of vulnerabilities. We operate a bug
bounty program to reward security researchers for discovering and
reporting issues.
This policy outlines how to report vulnerabilities, how our bug bounty
program works, and our approach to patching and disclosing security
issues.

------------------------------------------------------------------------

## Reporting a Vulnerability

**Private Disclosure:**
If you discover a potential security vulnerability in Cosmos (e.g.,
Cosmos SDK, CometBFT, IBC, or related core components), report it
privately through our official channels.

-   **Preferred method:** Report via the [Cosmos HackerOne Bug Bounty
    Program](https://hackerone.com/cosmos).
-   If unable to use HackerOne, you may email: `security@cosmoslabs.io`
    with the vulnerability details (steps to reproduce, impact, etc.).

> Issues reported via email are *ineligible* for bounty rewards --- only reports through HackerOne qualify.

When reporting, **do not publicize the issue** (e.g., no public GitHub
issues or social posts) until we have addressed it and granted
permission to disclose.
We may coordinate with you on a public disclosure timeline.

By reporting to us, you agree to **participate in coordinated
vulnerability disclosure**, allowing us time to develop and
distribute a fix before details are made public.

------------------------------------------------------------------------

## Bug Bounty Program Overview

Our bug bounty program rewards valid security bug reports submitted
through **HackerOne**, where bounty amounts depend on severity and
impact.

**Scope:** Core Cosmos Stack components, such as: Cosmos SDK, CometBFT, IBC, Cosmos EVM and
other critical infrastructure

For full scope, severity definitions, and reward ranges, see the Cosmos
page on [HackerOne](https://hackerone.com/cosmos).

We follow a **Safe Harbor** policy to protect researchers acting in good
faith. The official HackerOne page contains the **Coordinated
Vulnerability Disclosure Policy** and **Safe Harbor terms**.
> In case of discrepancies, the HackerOne policy supersedes other
documents.

------------------------------------------------------------------------

## Vulnerability Severity Levels

All reported vulnerabilities are assigned a severity category guiding how they are handled and disclosed.

| **Level**    | **Description**                                                                     | **Examples**                                            |
|--------------|-------------------------------------------------------------------------------------|---------------------------------------------------------|
| **Critical** | Bugs posing an existential or network-wide threat (fund loss, inflation, or theft). | Token creation beyond fixed supply, permanent fork bug. |
| **High**     | Major disruption to many nodes or users, often remotely exploitable.                | Remote crash or chain halt vulnerability.               |
| **Medium**   | Moderate impact or harder to exploit; may require specific configurations.          | Node halt requiring high permissions and access         |
| **Low**      | Minor impact or impractical exploitation.                                           | Slow block propagation, limited DoS.                    |

These levels align with common security practices and determine both
urgency and disclosure timelines. For more information, refer to our [Classification Matrix](./resources/CLASSIFICATION_MATRIX.md).

------------------------------------------------------------------------

## Silent Patch and Disclosure Process

Cosmos adopts a **silent patch** approach. Vulnerabilities are fixed
quietly before disclosure.
This mirrors practices from projects like **Ethereum's Geth**, **Bitcoin
Core**, and **Zcash**.

Announcing vulnerabilities too early can endanger unpatched nodes.
Silent fixes allow time for safe upgrades before attackers become aware.

### Fix Distribution

-   Fixes are incorporated into new or patch releases.
-   Release notes may **not** mention the security nature of the fix.
-   Validators and node operators are **privately encouraged** to
    upgrade.
-   For critical issues, patches may be **privately distributed** to key
    operators or trigger **emergency upgrades**.

### Disclosure Timeline


### Disclosure Timeline

| **Severity**     | **Disclosure Timing**                                                      | **Details**                                                                             |
|------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| **Low / Medium** | ~4 weeks after public fix release                                          | Publish full advisory with impact and fix details.                                      |
| **High**         | After the affected version reaches **End-of-Life (EOL)** (~1 year typical) | Delayed high-severity policy ensures attackers are not aware of exploits.               |
| **Critical**     | **Ad-hoc** (case-by-case)                                                  | Disclose only when safe; may delay or omit full details to prevent future exploitation. |

------------------------------------------------------------------------

## Transparency and Post-Disclosure

Once the embargo period expires, a **Security Advisory** is published
(via GitHub advisories or blog), detailing: - Vulnerability
description - Affected versions - Severity - Fix steps - Reporter credit
(unless anonymity requested)

Historical advisories remain publicly available.
This **delayed transparency model** balances immediate safety with
long-term openness and trust.

------------------------------------------------------------------------

Cosmos Labs deeply appreciates the work of white-hat hackers and auditors
whose contributions strengthen the Cosmos ecosystem.

------------------------------------------------------------------------

### References

-   [Bitcoin Core Security
    Advisories](https://bitcoincore.org/en/security-advisories/)
-   [Go Ethereum Vulnerability
    Disclosure](https://ethereumpow.github.io/go-ethereum/docs/vulnerabilities/vulnerabilities)
-   [Bitcoin Core Security Disclosure Policy
    Announcement](https://bitexes.com/blog/124272)
