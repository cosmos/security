## Disclosure Process

Cosmos uses the following disclosure process:

1. Once a security report is received, the Cosmos team works to verify the issue and confirm its severity level.
2. A Security Incident team is formed that collaborates with other core Cosmos teams as necessary to determine the vulnerability’s potential impact on users, zones, and the Cosmos Hub.
3. Patches are prepared for eligible releases of the software in private repositories. See “Supported Releases” in the SECURITY.md file of each relevant repository for more information on which releases are considered eligible.
4. If it is determined that a CVE-ID is required, we request a CVE through Github.
5. We provide the community with a 24-hour notice that a security release is impending, giving partners time to prepare their systems for the update. Notifications can include Discord, Telegram, Twitter, forum posts, and emails, including emails sent to the [Cosmos Security Mailing List](TODO).
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
