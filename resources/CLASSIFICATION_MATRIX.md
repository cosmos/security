# Interchain Stack Severity Classification Framework

**Version**: ACMv1.2

## Criticality Matrix

![./assets/crit_matrix.png](./assets/crit_matrix.png)

## Why Impact vs Likelihood

Using a framework such as the Impact vs. Likelihood matrix to bucket risk into five main categories: critical, high, medium, low, and informational, is an efficient way to communicate relative risk to other parties.

### Subjectivity and Contextualization

Unlike some complex risk assessment models, including CVSS, the Impact vs. Likelihood framework allows for a degree of subjectivity and contextualization. Engineers can tailor the assessment criteria to suit their specific needs and factors relevant to their operations. This flexibility enhances relevance and usefulness in various environments.

### Prioritization of Resources

By classifying risks based on their impact and likelihood, teams can allocate resources to address the most critical risks first. This approach enables them to focus on mitigating potential high-impact, high-likelihood risks, thereby minimizing their overall risk exposure.

### Quantitative and Qualitative

An Impact vs. Likelihood framework can be used in quantitative and qualitative risk assessments. While some teams may assign numerical values to impact and likelihood, others may use descriptive scales (e.g., low, medium, high). This adaptability applies to various teams with varying risk management maturity levels.

## Topics to consider when determining risk

### Availability

Evaluate the impact on the availability of the chain. Will the vulnerability lead to service disruptions, downtime, or denial of service? Consider the potential financial losses, reputational damage, and operational impacts of unavailable resources of the chain. Across the affected chains, how important is liveness to the affected groups?

### Recoverability

Analyze the ease and speed of recovery from exploiting the vulnerability. How quickly can the system or service be restored to regular operation? Assess the resources and efforts required for recovery and the impact on business continuity.

### Confidentiality

Determine if the vulnerability compromises sensitive information or data. Assess the potential damage if unauthorized parties gain access to sensitive data, including financial losses, legal consequences, and harm to customer trust. This area is less important in our space but may be critical for privacy-focused chains.

### Integrity

Consider the impact on data integrity if the vulnerability allows unauthorized modification or alteration of critical information. This may result in misinformation, data corruption, and potential legal or compliance issues.

### Authentication and Authorization Bypass

Evaluate if the vulnerability can lead to unauthorized access to privileged wallets or systems. Unauthorized access can enable attackers to gain control over critical assets or escalate their privileges, potentially leading to severe consequences.

### Data Loss

Determine if the vulnerability can result in data loss. Losing critical data can have significant financial, operational, and legal ramifications.

### Exploitation Complexity

Assess how difficult it is for an attacker to exploit the vulnerability. If the exploitation is straightforward, the risk is higher than a vulnerability requiring complex, sophisticated techniques. Does successful exploitation require governance or leave other noisy artifacts that could be detected?

### Scope

Consider the scope of the impact. Does the vulnerability affect a single system, multiple systems, or the entire chain or ecosystem?

### Regulatory and Compliance

Evaluate whether the vulnerability could result in non-compliance with relevant regulations or industry standards. Non-compliance may lead to penalties, legal actions, and reputational damage. Depending on the current regulatory environment, this may be more or less relevant (e.g., banned addresses, OFAC compliance, etc.)

### Dependencies and Interconnections

Examine the potential ripple effects of the vulnerability on interconnected systems or third-party services. One vulnerability could have cascading effects on various parts of the infrastructure. A good example is the ics23 bug, where the impact was very much inter-chain.

### Patch Availability and Remediation Effort

Consider the availability of patches or mitigations to address the vulnerability. If limiting the availability of a patch is required to limit impact, consider the effect on chains unable to patch and consider the tradeoffs. Additionally, the impact may be substantially more significant depending on the difficulty or complexity of patching this issue. Assess the effort and time required to remediate the issue effectively.

### Threat Landscape

Analyze the current threat landscape and whether known active exploits target the vulnerability. The presence of active exploits increases the urgency of addressing the issue.

### Token Supply and Circulating Supply

Vesting and locking mechanisms can affect the token supply and circulation. Locked tokens are typically excluded from the circulating supply, impacting metrics like market capitalization and token liquidity. A vulnerability in one of these mechanisms may adversely affect a chain's tokenomics implementation, leading to price fluctuations and shifts in market perception.

### Mitigation mechanisms

Investing in mechanisms, including a circuit breaker for specific APIs, may reduce the impact of vulnerabilities to all chains. This type of feature is immensely beneficial for systemic risk reduction. Does a mechanism exist today that chains know how to use that could mitigate this risk efficiently?

## Real-world Examples

- Critical

  - Likely, Catastrophic impact
  - Cross-chain impact and private, coordinated emergency patching required.
  - Consequences of a critical issue are typically irreversible, e.g. loss of funds, trivial minting of funds.
  - Examples include:
    - [Dragonberry](https://forum.cosmos.network/t/ibc-security-advisory-dragonberry/7702)
    - [ASA-2024-007](https://github.com/cosmos/ibc-go/security/advisories/GHSA-j496-crgh-34mx): Potential Reentrancy using Timeout Callbacks in `ibc-hooks`

- High

  - Possible likelihood, Considerable impact
  - Somewhat cross-chain impact, with consequences that are difficult to recover from and likely to require state modification. These consequences could include non-determinism that results in a trivial chain halt or bugs that undermine the economic model of the Interchain Stack.
  - Examples include:
    - [Pigeonfall](https://github.com/cosmos/ibc-apps/security/advisories/GHSA-q7m9-jcqg-g9pq): Packet Forward Middleware
    - [ASA-2024-001](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-2557-x9mg-76w8): Validation of `VoteExtensionsEnableHeight` can cause chain halt (CometBFT)

- Medium

  - Possible likelihood, Moderate impact
  - Affects specific chains using the feature,with consequences that are recoverable and provide moderate disruption to chain availability. The consequences could include business logic errors or missing validation that interrupts chain operations and inconveniences users, but the issue may not have cross-chain impact.
  - Examples include:
    - [ASA-2024-002](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-2557-x9mg-76w8): Default `PrepareProposalHandler` may produce invalid proposals when used with default `SenderNonceMempool` (Cosmos SDK)

- Low
  - Possible likelihood, Marginal impact
  - Affects some chains using the feature, with consequences that can be recovered from without significantly disrupting chain availability. The consequences could include misconfigured chain invariants that impact chain performance in specific use cases or improper error handling.
  - Examples include:
    - [ASA-2023-002](https://github.com/cometbft/cometbft/security/advisories/GHSA-hq58-p9mv-338c): Default for BlockParams.MaxBytes consensus parameter may increase block times and affect consensus participation (CometBFT)
    - [ASA-2024-005](https://github.com/cosmos/cosmos-sdk/security/advisories/GHSA-86h5-xcpx-cfqc): Potential slashing evasion during re-delegation (Cosmos SDK)
    - Interchain Account Squatting

## Guidance for Chain Developers and Validators

Generally, while any security issue classified as Low or Medium severity does have a security impact, we recommend patching issues of these severities in your chain’s regular software upgrade governance process. If a Low or Medium issue poses a higher risk to your chain due to its use case, however, an expedited network upgrade may be appropriate.

Security issues classified as High or Critical severity will have significant consequences, and as such they will generally require Emergency Security Coordination or Emergency Security Upgrades to impacted networks.

- In the event of security coordination for a **High** severity vulnerability, if impacted, your network should be prepared to upgrade using expedited upgrade processes immediately after a public patch release of the affected component is available.

- In the event of security coordination for a **Critical** vulnerability, your network should be prepared to privately contact validators to privately distribute and coordinate patching without publicly disclosing the vulnerability in a software release. During private emergency coordination with impacted parties, we strongly discourage network operators from sharing patches with others in the community as this risks full disclosure and exploitation of the respective vulnerability.

Emergency Security Coordination or Emergency Security Upgrades should be reserved for High and Critical issues, or issues that pose significant risk to your use case.

## Vulnerability Disclosure and Emergency Security Coordination

If you believe that you have found a vulnerability in the Interchain Stack or would like to contribute to the Cosmos Bug Bounty Program by reporting a bug, please see [https://hackerone.com/cosmos](https://hackerone.com/cosmos). This Severity Classification Framework is used to assess all vulnerabilities reported to the bug bounty program.

If you are building on the Interchain Stack and want to ensure that your team is easy to contact in the event that you are impacted by a Critical security vulnerability, create a security contact email alias and include this information in a `security.md` in your main code repository.

If you are interested in receiving security advisories about vulnerabilities discovered in the Interchain Stack, sign up for the security email distribution list [here](https://interchaincirt.org/signup).

If you are a chain operator and you want to verify if Emergency Security Coordination for an Interchain Stack component is taking place, please reach out to our official channel by emailing [security@interchain.io](mailto:security@interchain.io). Though our team cannot make public announcements about private security coordination activities, we can privately confirm if any emergency coordination is actively taking place.

### Changelog

- ACMv1.2: Change "Critical" imapct to "Considerable" to avoid confusion with Severity rating. The impact captured before and after this change is the same.

[Security Classification Matrix](https://github.com/interchainio/security/blob/main/resources/CLASSIFICATION_MATRIX.md) © 2024 by Amulet is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1)
