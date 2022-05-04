# Security

This security document outlines the Coordinated Vulnerability Disclosure Policy that the Cosmos team follows regarding security issues 
that can impact partners and users of the Cosmos technology, including
Cosmos-based zones and the Cosmos Hub itself.

> **IMPORTANT**: If you find a security issue, 
please report it to our [bug bounty program](https://hackerone.com/cosmos) on HackerOne. *DO NOT* open a public issue on the repository.

## Scope

In scope are all the core repositories of the Cosmos stack, including:

- [Tendermint Core](https://github.com/tendermint/tendermint)
- [Cosmos-SDK](https://github.com/cosmos/cosmos-sdk)
- [IBC-Go](https://github.com/cosmos/ibc-go)
- [Gaia (Cosmos Hub)](https://github.com/cosmos/gaia)

What follows is a general description of the security process that applies to
all repositories. Please see the SECURITY.md files in each repository for any additional details specific to that repository.

## Prerequisites

If a vulnerability and its exploit are both publicly known, the security process may not apply. 
However, in such cases, resolutions and mitigation strategies may still be eligible for rewards through a bounty program.

## Reporting a Bug

As part of our Coordinated Vulnerability Disclosure
Policy, we operate a [bug bounty](https://hackerone.com/cosmos) on HackerOne.
Please see the bug bounty page for more details on submissions and rewards, and see "Example Vulnerabilities" 
in the respective SECURITY.md files of all repositories in scope for examples of the kinds of bugs we're most interested in.

### Guidelines

We require that all researchers:

* Use the bug bounty to disclose all vulnerabilities, and avoid posting vulnerability information in public places, including Github, Discord, Telegram, and Twitter
* Make every effort to avoid privacy violations, degradation of user experience, disruption to production systems (including but not limited to the Cosmos Hub), and destruction of data
* Keep any information about vulnerabilities that you’ve discovered confidential between yourself and the Cosmos engineering team until the issue has been resolved and disclosed
* Avoid posting personally identifiable information, privately or publicly

If you follow these guidelines when reporting an issue to us, we commit to:

* Not pursue or support any legal action related to your research on this vulnerability
* Work with you to understand, resolve and ultimately disclose the issue in a timely fashion

## Disclosure Process

Cosmos uses the following disclosure process:

1. Once a security report is received, the Cosmos team works to verify the issue and confirm its severity level.
2. A Security Incident team is formed that collaborates with other core Cosmos teams as necessary to determine the vulnerability’s potential impact on users, zones, and the Cosmos Hub.
3. Patches are prepared for eligible releases of the software in private repositories. See “Supported Releases” in the SECURITY.md file of each relevant repository for more information on which releases are considered eligible.
4. If it is determined that a CVE-ID is required, we request a CVE through Github.
5. We provide the community with a 24 hour notice that a security release is impending, giving partners time to prepare their systems for the update. Notifications can include Discord, Telegram, Twitter, forum posts, and emails, including emails sent to the [Cosmos Security Mailing List](TODO).
6. 24 hours following this notification, the fixes are applied publicly and new releases are issued.
7. Once new security releases are available, we notify the community, through the same channels as above. <!-- We also publish a Security Advisory on Github and publish the CVE, as long as neither the Security Advisory nor the CVE include any information on how to exploit these vulnerabilities beyond what information is already available in the patch itself. -->
8. Once the community is notified, we will pay out any relevant bug bounties to submitters.
9. Approximately one week after the releases go out, we will publish a post with further details on the vulnerability as well as our response to it. This timeline may be adjusted depending on the severity of the issue and the need to inform and update partners.

This process can take some time. Every effort will be made to handle the bug in as timely a manner as possible, however it's important that we follow the process described above to ensure that disclosures are handled consistently and to keep Cosmos and its downstream dependent projects--including but not limited to the Cosmos Hub--as secure as possible.

### Disclosure Communications

Communications will include the following details:
1. Affected version(s)
1. New release version
1. Impact on user funds
1. For timed releases, a date and time that the new release will be made available
1. Impact on users, including zones and the Cosmos Hub, if upgrades are not completed in a timely manner
1. Potential actions to take if an adverse condition arises during the security release process

An example notice looks like:

```
Dear Cosmos Hub Validators,

A critical security vulnerability has been identified in Gaia v4.0.x. 
User funds are NOT at risk; however, the vulnerability can result in a chain halt.

This notice is to inform you that on [[**March 1 at 1pm EST/6pm UTC**]], we will be releasing Gaia v4.1.x, which patches the security issue. 
We ask all validators to upgrade their nodes ASAP.

If the chain halts, validators with sufficient voting power need to upgrade and come online in order for the chain to resume.
```

### Example Timeline

The following is an example timeline for the triage and response. The required roles and team members are described in parentheses after each task; however, multiple people can play each role and each person may play multiple roles.

#### 24+ Hours Before Release Time

1. Request CVE number (ADMIN)
1. Gather emails and other contact info for validators (COMMS LEAD)
1. Create patches in a private security repo, and ensure that PRs are open targeting all relevant release branches (TENDERMINT ENG, TENDERMINT LEAD)
1. Test fixes on a testnet  (GAIA ENG, TENDERMINT ENG, COSMOS SDK ENG)
1. Write “Security Advisory” for forum (GAIA LEAD)

#### 24 Hours Before Release Time

1. Post “Security Advisory” pre-notification on forum (GAIA LEAD)
1. Announce security advisory/link to post in various other social channels (Telegram, Discord) (COMMS LEAD)
1. Send emails to validators or other users (PARTNERSHIPS LEAD)

#### Release Time

1. Cut software releases for eligible versions of all affected software (TENDERMINT ENG)
1. Post “Security releases” on forum (GAIA LEAD)
1. Remind everyone via social channels (Telegram, Discord)  that the release is out (COMMS LEAD)
1. Send emails to validators or other users (COMMS LEAD)
1. Publish Security Advisory and CVE, if CVE has no sensitive information (ADMIN)

#### After Release Time

1. Write forum post with exploit details (GAIA LEAD)
2. Approve pay-out on HackerOne for submitter (ADMIN)

#### 7 Days After Release Time

1. Publish CVE if it has not yet been published (ADMIN)
2. Publish forum post with exploit details (GAIA ENG, GAIA LEAD)

