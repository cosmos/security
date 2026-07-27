# Cosmos Stack Severity Classification Framework

**Version**: v1.3

## Impact Scenarios Framework

Our severity classifications are simply done by matching a security report's
demonstrated, deterministic impact to a set of impacts that we care about most.
Each of those listed impacts comes with a predetermined severity, available for
all to see.

This explicit listing of impacts and their predetermined severities is done to
reduce subjectivity and increase transparency in our program, helping security
researchers get paid out faster and know upfront how their security report will
be classified.

See the [Cosmos Program Immunefi Impacts in
Scope](https://immunefi.com/bug-bounty/cosmos/scope/#top) section for more
details.

### Downgrade Scenarios

While the impact scenarios framework aims to be as simple as possible and
associate an on-chain or off-chain impact to a severity classification, it
ignores the other half of the equation, the likelihood of the impact occurring.
Not all security reports of a single impact will always be as likely to happen,
which must be taken into account to offer fair rewards when comparing two
reports against each other.

To take these variables into account, we have listed explicit scenarios that
would downgrade the severity of a predefined impact. A non-exhaustive set of
downgrade scenarios may be:
* For the impact to take place, it requires the malicious actor to be part of a permissioned set of users.
* For the impact to take place, it requires a tight race condition to occur that the malicious actor cannot reliably control.
* For the impact to take place, it requires some optional module to be enabled on an honest user's chain.

## Guidance for Chain Developers and Validators

Generally, while any security issue classified as Low or Medium severity does have a security impact, we recommend patching issues of these severities in your chain’s regular software upgrade governance process. If a Low or Medium issue poses a higher risk to your chain due to its use case, however, an expedited network upgrade may be appropriate.

Security issues classified as High or Critical severity will have significant consequences, and as such they will generally require Emergency Security Coordination or Emergency Security Upgrades to impacted networks.

- In the event of security coordination for a **High** severity vulnerability, if impacted, your network should be prepared to upgrade using expedited upgrade processes immediately after a public patch release of the affected component is available.

- In the event of security coordination for a **Critical** vulnerability, your network should be prepared to privately contact validators to privately distribute and coordinate patching without publicly disclosing the vulnerability in a software release. During private emergency coordination with impacted parties, we strongly discourage network operators from sharing patches with others in the community as this risks full disclosure and exploitation of the respective vulnerability.

Emergency Security Coordination or Emergency Security Upgrades should be reserved for High and Critical issues, or issues that pose significant risk to your use case.

## Vulnerability Disclosure and Emergency Security Coordination

If you believe that you have found a vulnerability in the Cosmos Stack or would like to contribute to the Cosmos Bug Bounty Program by reporting a bug, please see [https://hackerone.com/cosmos](https://hackerone.com/cosmos). This Severity Classification Framework is used to assess all vulnerabilities reported to the bug bounty program.

If you are building on the Cosmos Stack and want to ensure that your team is easy to contact in the event that you are impacted by a Critical security vulnerability, create a security contact email alias and include this information in a `security.md` in your main code repository.

If you are interested in receiving security advisories about vulnerabilities discovered in the Cosmos Stack, sign up for the security email distribution list [here](https://interchaincirt.org/signup).

If you are a chain operator and you want to verify if Emergency Security Coordination for an Cosmos Stack component is taking place, please reach out to our official channel by emailing [security@cosmoslabs.io](mailto:security@cosmoslabs.io). Though our team cannot make public announcements about private security coordination activities, we can privately confirm if any emergency coordination is actively taking place.

### Changelog

- v1.3: Update severity classification framework from Impact vs Likelihood to explicit impact scenarios with severity downgrade conditions.
- ACMv1.2: Change "Critical" impact to "Considerable" to avoid confusion with Severity rating. The impact captured before and after this change is the same.

[Security Classification Matrix](https://github.com/interchainio/security/blob/main/resources/CLASSIFICATION_MATRIX.md) © 2024 by Amulet is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1)
