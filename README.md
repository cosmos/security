# Cosmos Maintenance and Security

This repository holds the artifacts and references behind maintenance and
security of the Cosmos Stack: published advisories, third-party audits, incident
communications, the severity classification framework, and the release and
maintenance policy.

Vulnerabilities are not reported here. See below.

## Reporting a vulnerability

Report through the
[Cosmos Immunefi Bug Bounty Program](https://immunefi.com/bug-bounty/cosmos/information/).
That is the only route eligible for a bounty.

Never open a public issue, pull request, or discussion for a suspected
vulnerability.

[security@cosmos.network](mailto:security@cosmos.network) is monitored
continuously for security coordination with chains and partners. Reports that
arrive there are acted on, but they are not eligible for a bounty.

The full policy, covering how reports are handled, how fixes are distributed,
when details are disclosed, and what happens if someone publishes ahead of the
disclosure date, is served to every repository in the organization from
[cosmos/.github/SECURITY.md](https://github.com/cosmos/.github/blob/main/SECURITY.md).

## Receiving patches privately

Teams running the Cosmos Stack in production can sign up for private security
notifications by filling out
[this form](https://forms.gle/7scaqTEmxXzXbpfR6).

Signing up is the first step, not access itself. Receiving fixes before they are
public additionally requires completing KYC, which is arranged by email with
[security@cosmos.network](mailto:security@cosmos.network).

## Policies

| Policy | Where it lives |
| --- | --- |
| Vulnerability disclosure and bug bounty | [cosmos/.github/SECURITY.md](https://github.com/cosmos/.github/blob/main/SECURITY.md) |
| Severity classification | [resources/CLASSIFICATION_MATRIX.md](./resources/CLASSIFICATION_MATRIX.md) |
| Release families, support windows, retirement | [docs.cosmos.network](https://docs.cosmos.network/sdk/latest/release-family) |
| Release and maintenance | [POLICY.md](./POLICY.md) |
| Code of Conduct | [cosmos/.github/CODE_OF_CONDUCT.md](https://github.com/cosmos/.github/blob/main/CODE_OF_CONDUCT.md) |
| Contributing | [cosmos/.github/CONTRIBUTING.md](https://github.com/cosmos/.github/blob/main/CONTRIBUTING.md) |

The disclosure policy, code of conduct, and contributing guide live in
`cosmos/.github` so that every repository in the organization serves the same
copy. They are not duplicated here.

## What is in this repository

| Path | Contents |
| --- | --- |
| [ADVISORIES.md](./ADVISORIES.md) | Every ASA advisory issued to date, linked to its GHSA |
| [audits/](./audits) | Third-party audit reports, by component |
| [communications/](./communications) | Incident post mortems, and pre-notifications with their detached signatures |
| [reports/](./reports) | Transparency reports |
| [resources/](./resources) | Severity classification framework and liveness guidance |
| [release/](./release) | Release signing keys |

## A note on liveness

The Cosmos Stack is built on safety over liveness and does not offer distributed
performance guarantees. [resources/LIVENESS.md](./resources/LIVENESS.md) sets out
what that means for anyone building on it.
