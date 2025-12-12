# Cosmos Security Vulnerability Disclosure and Bug Bounty Policy

## Introduction

Cosmos Labs is committed to maintaining the security of the Cosmos Stack
and supporting responsible vulnerability disclosure. We operate a bug
bounty program to incentivize security researchers to identify and
report security issues.

This document defines the process for reporting vulnerabilities,
describes the bug bounty program, and outlines Cosmos Labs’ approach to
patching and public disclosure.

------------------------------------------------------------------------

## Reporting a Vulnerability

**Private Disclosure Required**

Security vulnerabilities affecting the Cosmos ecosystem—including the
Cosmos SDK, CometBFT, IBC, and other core components—must be reported
privately through the channels listed below.

- **Preferred:** Submit reports through the
  [Cosmos HackerOne Bug Bounty Program](https://hackerone.com/cosmos).
- If HackerOne submission is not possible, reports may be sent to
  `security@cosmoslabs.io` with sufficient technical detail, including
  impact and reproduction steps.

> Reports submitted via email are *not eligible* for bounty rewards.
> Only reports submitted through HackerOne qualify for bounties.

Public disclosure of vulnerabilities (including GitHub issues, blog
posts, or social media) is prohibited until Cosmos Labs has remediated
the issue and explicitly authorized disclosure.
Disclosure timelines may be coordinated with the reporter.

Submission of a report constitutes agreement to participate in
**coordinated vulnerability disclosure**, allowing time for development,
testing, and deployment of a fix prior to public release of details.

------------------------------------------------------------------------

## Bug Bounty Program Overview

Cosmos Labs operates a bug bounty program through **HackerOne**.
Eligible reports are rewarded based on severity, impact, and quality.

**In Scope:** Core Cosmos Stack components, including the Cosmos SDK,
CometBFT, IBC, Cosmos EVM, and other critical infrastructure components.

The authoritative scope definition, severity classifications, and
reward ranges are maintained on the Cosmos
[HackerOne program page](https://hackerone.com/cosmos).

The program is governed by **Safe Harbor** provisions for good-faith
research. The HackerOne page defines the applicable **Coordinated
Vulnerability Disclosure Policy** and **Safe Harbor terms**.

> In the event of conflict, the HackerOne policy supersedes all other
> documentation.

------------------------------------------------------------------------

## Vulnerability Severity Levels

Reported vulnerabilities are assigned a severity classification that
determines handling priority and disclosure timing.

| **Level**    | **Description**                                                                     | **Examples**                                            |
|--------------|-------------------------------------------------------------------------------------|---------------------------------------------------------|
| **Critical** | Network-wide or existential threats, including fund loss, inflation, or theft.     | Unlimited token minting, permanent consensus failure.   |
| **High**     | Severe impact affecting many nodes or users; often remotely exploitable.            | Remote crash or chain halt vulnerabilities.             |
| **Medium**   | Limited or conditional impact; exploitation may require specific conditions.        | Node halt requiring elevated permissions.               |
| **Low**      | Minor impact or impractical exploitation scenarios.                                 | Slow block propagation, limited denial-of-service.      |

These classifications follow industry standards and inform response
urgency and disclosure policy. Additional details are available in the
[Classification Matrix](./resources/CLASSIFICATION_MATRIX.md).

------------------------------------------------------------------------

## Silent Patch and Disclosure Process

Cosmos Labs follows a **silent patch** model for security vulnerabilities.
Issues are addressed privately and remediated prior to public
disclosure. This approach is consistent with established practices used
by projects such as **Ethereum Geth**, **Bitcoin Core**, and **Zcash**.

Premature disclosure can place unpatched networks at risk. Silent
remediation allows operators time to upgrade before vulnerability
details become public.

### Fix Distribution

- Fixes are delivered through patch or minor releases.
- Release notes may omit explicit references to security implications.
- Validators and node operators may be notified privately to upgrade.
- For critical vulnerabilities, fixes may be distributed privately to
  key operators or require emergency network upgrades.

### Disclosure Timeline

| **Severity**     | **Disclosure Timing**                                                      | **Details**                                                                             |
|------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| **Low / Medium** | Approximately four weeks after public release of the fix                  | Full advisory published with impact and remediation details.                            |
| **High**         | After the affected version reaches **End-of-Life (EOL)** (~1 year typical) | Disclosure delayed to reduce exploitation risk.                                         |
| **Critical**     | Case-by-case                                                                | Disclosure only when deemed safe; details may be limited or withheld.                   |

------------------------------------------------------------------------

## Transparency and Post-Disclosure

After expiration of the disclosure embargo, Cosmos Labs publishes a
**Security Advisory** (via GitHub advisories or official blog posts)
containing:

- Vulnerability description
- Affected versions
- Severity classification
- Remediation guidance
- Reporter attribution (unless anonymity is requested)

All advisories remain publicly available. This delayed disclosure model
balances ecosystem safety with long-term transparency.

------------------------------------------------------------------------

Cosmos Labs acknowledges and appreciates the contributions of security
researchers, auditors, and white-hat hackers who strengthen the Cosmos
ecosystem.

------------------------------------------------------------------------

### References

- [Bitcoin Core Security Advisories](https://bitcoincore.org/en/security-advisories/)
- [Go Ethereum Vulnerability Disclosure](https://ethereumpow.github.io/go-ethereum/docs/vulnerabilities/vulnerabilities)
- [Bitcoin Core Security Disclosure Policy Announcement](https://bitexes.com/blog/124272)
