# Cosmos EVM GHSA-7g4w-cg88-2cq2 Post-Mortem

Date: 2026-08-28  
GHSA: [GHSA-7g4w-cg88-2cq2](https://github.com/cosmos/evm/security/advisories/GHSA-7g4w-cg88-2cq2)

## Summary

Between August 20, 2026, 19:06 UTC, and August 25, 2026, 15:20 UTC, attackers exploited a vulnerability in Cosmos EVM to steal funds from multiple Cosmos-based blockchains. After MANTRA notified Cosmos Labs that the vulnerability was being actively exploited on its network, the Cosmos security team initiated its exploit response across all known Cosmos EVM networks, distributed patch and mitigation guidance through secure private channels, and coordinated with forty Cosmos chains to assess exposure and mitigate impact. 

Six networks were exploited. Attackers exchanged stolen tokens for approx. USD 2.87M in various other assets on DEXes, based on August 19 prices. In addition, an estimated USD 2.85M was sold on centralized exchanges, based on publicly available volume data.  As of the time of publishing, the centralized exchange accounts the attackers used have been frozen pending investigation by the relevant authorities. Cosmos Labs collaborated with thirteen other potentially exposed networks to patch, halt, or apply other mitigations without further incidents. We are continuing to work with authorities, researchers, and affected chains to assist in recovery efforts. 

The underlying vulnerability had been reported through the Cosmos Bug Bounty Program and initially assessed as not presenting a risk of fund loss to production network configurations. Based on that assessment, Cosmos Labs addressed the vulnerability through its silent, public patch process rather than the private patch distribution process used when a vulnerability is believed to threaten live user funds. 

The scale and decentralized nature of the Cosmos open source ecosystem make cybersecurity particularly important and challenging. The code path had been audited by internal review and external independent firms. The resulting discovered vulnerabilities were either remediated or accepted prior to release of the code. The vulnerability exploited in this situation was not discovered in the process of these audits. Since January 2025, Cosmos Labs has triaged thousands of vulnerability reports, paid more than $850,000 to security researchers through its Bug Bounty Program, and patched dozens of vulnerabilities through public, silent and private patch processes. This incident exposed areas where these systems need to improve. 

Immediately, Cosmos Labs will make comprehensive changes to triage and remediation of critical vulnerabilities. This will involve developing more robust approaches to identify cases where the vulnerability scope exceeds what the original report documented, as in this case. Cosmos Labs will also increase awareness of security-critical coordinated vulnerability disclosure (CVD) channels across all Cosmos developer-facing properties, perform and optimize against regular health checks for developer responsiveness to these channels, and further define public standards for how and when these channels are used. Long term, Cosmos Labs will conduct a thorough audit of security practices in partnership with external experts to identify additional opportunities to improve the ecosystem’s security. 

This report discusses the exploit, its impact, the factors that contributed to the incident, and commitments for change. 

## Discussion of the exploit

The exploit affected Cosmos EVM chains running versions below `v0.6.2` or `v0.7.2` in production. In practical terms, the attacker exploited an inconsistency between how Cosmos EVM and the Cosmos SDK accounted for certain token balances. By combining two vulnerabilities into a single transaction, the attacker could manipulate those balances and extract legitimate tokens from vesting accounts without creating a corresponding increase in total token supply.

The underlying vulnerabilities were in the shared `cosmos/evm` code that reconciles EVM state with the Cosmos x/bank module. The first vulnerability is that when a vesting account delegates through the staking precompile, the post-delegation balance write-back could underflow. Specifically, this would happen when a vesting account delegates more than its spendable balance. 

The Cosmos EVM’s `StateDB` only tracks an account's spendable balance; however, vesting accounts in Cosmos SDK state have both a spendable balance and a locked balance. The x/staking module and the EVM’s staking precompile allow for a vesting account to delegate *both* its spendable balance and its locked balance. The first vulnerability is that when delegating greater than the vesting account's spendable balance (i.e., its locked balance), an unchecked underflow in the EVM StateDB’s `SubBalance` function occurred, causing the vesting account’s balance to wrap to \~2^256. 

The second vulnerability was exploitable as a result of the balance underflow: the attacker used the underflowed balance. to overflow a victim account's balance. The underflowed balance, \~2^256  tokens, was sent to a victim account. This passed checks and requirements because those  tokens existed at that point and were considered valid. The victim accounts were arbitrary accounts with high balances, such as the *0x00* address or a multisignature wallet created during the chain genesis. The result of sending the 2^256 \- balance(victim) tokens was an overflow that netted out such that the attacker was left with the victim’s balance and the victim account was left with 0 tokens.

This attack demonstrated different behavior across EVM versions. 0.6.x lines use Mint/Burn on the backing SDK ledger, whereas 0.7.x directly sets balances within the x/bank module. On 0.6.x chains, the large mint of tokens would cause a supply overflow that would halt the chain, whereas 0.7.x chains would accept balance changes from the EVM as long as they can survive a uint256-to-int256 conversion.

To trigger both vulnerabilities in a single transaction, the attacker chained the first vulnerability (the balance underflow) and the second vulnerability (the balance overflow) via a malicious contract deployed on top of a vesting account, resulting in a net supply change of 0\. The attacker first precomputed the address the contract would be created at (since it is deterministic), then created a vesting account at that address, and finally deployed the malicious contract there. This malicious contract and vesting account setup allowed the attacker to execute both the underflow (via a delegation of the contract’s/vesting account’s locked balance, which is greater than the EVM’s view of the spendable balance), and the overflow of the victim account within a single supply-neutral transaction. After executing the exploit, the attacker used multiple bridges to move funds off affected chains and multiple exchanges to swap those assets for stablecoins and other tokens.

## Impact of the exploit

As of publication, Cosmos Labs is aware of six chains on which this exploit was leveraged by a rogue actor. Based on publicly available on-chain data, approximately USD 2.87 million in affected assets were subsequently bridged off affected chains and sold on DEXes. The underlying figures have been provided to us by the affected chains and are consistent with estimates based on available information, but have not been independently audited: 2,613,674.48 USDT, 114.129045 ETH, 93.78 TON, 1.393618 USDC, and 98.87 OSMO. In all of these cases, the attackers transferred the funds to other networks via bridges and exchanged them for stablecoins and other tokens, including WETH.	

Additional assets were deposited and sold on centralized exchanges for an estimated USD 2.85 million. As of the time of publishing, affected chains have reported to Cosmos Labs that the centralized exchange accounts used by the attackers have been frozen pending police investigation. 

Cosmos Labs is also coordinating with an additional network that, according to the affected team, halted before attackers were able to withdraw affected funds from the chain or exchange the assets anywhere. Further details have not been confirmed.  

## Factors that contributed to the exploit 

The following section examines the technical assumptions, internal processes, and ecosystem coordination challenges relevant to this exploit. We are documenting these factors to identify specific areas where we intend to strengthen our security practices going forward. Our hope is that this facilitates forward-looking collaboration with the open source ecosystem that leads to improvements in the ecosystem’s security posture. 

The Cosmos ecosystem spans over 115 different known public blockchains. Since the Cosmos software is open source and permissionless to deploy, Cosmos Labs does not have a complete and accurate registry of every network using Cosmos. In some cases, Cosmos Labs becomes aware of deployments only through public channels. During this exploit, we learned of eleven additional deployments of Cosmos EVM that had not previously registered with our security communication channels, which were identified and contacted. As described in the Takeaways section below, Cosmos Labs intends to expand its outreach and communication infrastructure to improve coverage across the ecosystem. 

### Determinations leading to patching the vulnerability in public

For this attack, the initial bug bounty report from April 25th included a PoC of the vulnerability for a Cosmos EVM network with 6-decimals. After receiving the report, the Cosmos Labs team made multiple attempts to reproduce the vulnerability on additional network configurations using our standard vulnerability testing process. We were unable to reproduce the vulnerability on 18-decimal networks and incorrectly concluded that it affected only non-18-decimal networks. All known production Cosmos EVM networks used 18-decimal configurations, and based on this testing, the risk assessment concluded the vulnerability did not threaten user funds on live networks.

As a result, the team began to patch the vulnerability according to the [silent patch process](https://docs.cosmos.network/sdk/latest/security/bug-bounty#silent-patch-and-disclosure-process) for issues that do not cause fund loss on production chains. In line with that policy, a patch was released publicly on the main branch of cosmos/evm in May. This patch was not immediately backported to release branches because it was state-breaking and would require chains to perform coordinated upgrades, which is not a typical requirement for patch releases. Instead,  the team planned to push the patch into the next minor release when developers would expect a coordinated upgrade.

In early August, additional reports from independent security researchers provided additional information that enabled the team to reproduce the vulnerability more broadly. The team then confirmed that all Cosmos EVM chains, regardless of decimal configuration, were affected and began to triage the vulnerability accordingly. At this point, for a vulnerability that is known to threaten user funds in production networks, the team would typically use secure channels to distribute a patch privately to the affected networks. Because the patch had already been publicly available on the main branch without known exploitation, the team concluded that it would be safe to proceed with the silent patch process  In line with that policy, the patch was obfuscated and backported to the `v0.6.x` and `v0.7.x` release branches of `cosmos/evm` and published in `v0.6.2` and `v0.7.2` respectively, with release notes that mention security without describing urgency or severity. 

### Third-Party Publication of Exploit Path 

Effective silent patching depends on the security significance of a patch and the methods for exploiting the underlying vulnerability not being readily identifiable, even when the relevant code is publicly available. 

However, on 2026-08-20 at 07:16 UTC, before the first known incident began, a public pull request in Push Chain's fork of Cosmos EVM ([pushchain/push-chain-evm\#40](https://github.com/pushchain/push-chain-evm/pull/40)) described the vulnerability and its exploitation path in detail, attributed the finding to an independent Hacken audit, and included a table identifying which released tags remained vulnerable. The pull request does not reference v0.6.2 or v0.7.2, and states that upgrading to a released tag would not remediate the issue. 

The publication of a vulnerability and exploit path in public by a downstream developer is highly unusual and can increase the risk of an exploit.  We ask that all developers be mindful of the risks of such posts and request that they submit potential vulnerabilities via the [Cosmos Immunefi Bug Bounty Program](https://immunefi.com/bug-bounty/cosmos/information/) coordinated disclosure process. Cosmos Labs has released patches for 37 vulnerabilities silently in the last 13 months without downstream developers precisely describing exploit paths in public. 

### Exploit remediation and outreach efforts

Cosmos Labs first became aware of the MANTRA halt through our security email ([security@cosmoslabs.io](mailto:security@cosmoslabs.io)). The MANTRA team notified the Cosmos Labs team that they had been exploited and quickly set up a war room with our team. This war room was used to discuss the exploit and determine that it was due to the vulnerability remediated by the recently released underflow patch in `v0.6.2`/`v0.7.2`. 

After this determination, the secure mailing list of known Cosmos EVM chains was used to distribute a notification informing chains that there is a critical vulnerability being actively exploited in public, that is patched by `v0.6.2` and `v0.7.2`, and urging them to upgrade to those releases. This was done \~2 hours after MANTRA's initial report that they had been exploited, and it was sent to all teams using Cosmos EVM that had provided their security team contact information for the security email list. In parallel, Cosmos Labs began independently analyzing the exploit to confirm the attack path and determine whether additional networks were at risk. 

About 45 hours after the MANTRA exploit, a message from TAC was received on Telegram notifying us that they had also been exploited. The TAC team had received the prior communication about upgrading due to the vulnerability.

This second exploit indicated a systematic attack on the ecosystem. Just over an hour after we were informed of the TAC exploit, another security notification was sent out to both the security mailing list and the shared Slack channel with Cosmos EVM users. This informed chains of an additional chain being exploited, and recommended that all chains running Cosmos EVM halt immediately. Cosmos Labs expanded outreach beyond its existing security contact list to identify and contact additional Cosmos EVM operators. About an hour later, we were notified by KiiChain via Slack that they had also been exploited.

Outreach has continued since then. Efforts have been focused on sharing mitigation information to defend against any additional attacks, encouraging chains to sign up for the security mailing list as well as re-informing them of our recommendation to halt and upgrade to prevent the ongoing exploits in the ecosystem. Another halt notification was sent to a larger mailing list after \~20 more verified individuals were added to the list, as well as reaching out to teams across established community channels, including X, Telegram, Discord, and email.

Prior to this exploit, the Cosmos EVM codebase had been reviewed by external parties and had an established disclosure process. Sherlock audited the code and published the [Interchain Labs Collaborative Audit Report](https://sherlock-files.ams3.digitaloceanspaces.com/reports/2025.07.28%20-%20Final%20-%20Interchain%20Labs%20Collaborative%20Audit%20Report%201753733572.pdf) in July 2025\. Cosmos Labs also operates a bug bounty program, in which the Cosmos EVM is in scope. Since May 2025, three critical vulnerabilities in Cosmos EVM have been disclosed and resolved through our bug bounty process: [ISA-2025-004](https://github.com/cosmos/evm/security/advisories/GHSA-mjfq-3qr2-6g84), [GHSA-8pfh-j44r-f654](https://github.com/cosmos/evm/security/advisories/GHSA-8pfh-j44r-f654), and [ASA-2026-002](https://github.com/cosmos/evm/security/advisories/GHSA-54gx-3cgr-7mfm).

## Timeline

All times UTC.

### Initial fix development and releases

**2026-04-25**

- The vulnerability is reported via the bug bounty program on HackerOne. Based on the information available at the time, including testing against production network configurations, the vulnerability is assessed as not resulting in fund loss on any configurations used by known production chains.

**2026-05-15**

- **13:32:37** — As a result of the classification as not causing fund loss on production chains, the fix is merged to the main branch: [\#1176](https://github.com/cosmos/evm/pull/1176) (SubBalance underflow guard). This is consistent with the [Silent patch process for issues that do not cause fund loss on production chains.](https://docs.cosmos.network/sdk/latest/security/bug-bounty#silent-patch-and-disclosure-process) 

**2026-05-15 \- 2026-08-13**

- Additional reports of the same vulnerability arrive from independent researchers.  
- The team used this new information to confirm that all Cosmos EVM chains, regardless of decimal configuration, were affected and began to triage the vulnerability accordingly.

**2026-08-19**

- Given that the patch had already been available on main without exploit, a determination is made to obfuscate and backport the patch to release branches to reduce the risk of it being picked up by bad actors, and publish it in releases, per the silent patch process.   
- **16:49:08** — [\#1253](https://github.com/cosmos/evm/pull/1253) backports \#1176 to `release/v0.6.x` (commit `82b3ef6c8`).  
- **17:53:17** — [\#1254](https://github.com/cosmos/evm/pull/1254) backports \#1176 to `release/v0.7.x` (commit `0182da198`).  
- **23:01:27** — [v0.6.2](https://github.com/cosmos/evm/releases/tag/v0.6.2) published.  
- **23:01:54** — [v0.7.2](https://github.com/cosmos/evm/releases/tag/v0.7.2) published.

**2026-08-20**

- **07:16:09** — A public pull request in Push Chain's fork of cosmos/evm ([pushchain/push-chain-evm\#40](https://github.com/pushchain/push-chain-evm/pull/40)) precisely describes the vulnerability and its exploitation path, attributes the finding to an independent Hacken audit, and identifies the affected release tags. 

### Exploit and Remediation

The timeline below outlines exploit and remediation for the first chains exploited, MANTRA, TAC, and KiiChain.

**2026-08-20**

- **19:06:00** — MANTRA attack \#1 ([tx 0xdf4947ad…](https://explorer.mantrachain.io/tx/0xdf4947ad49d8cf873f8dff98eafb0bdb65da6f5e2987dcb4b6b20b44f0971a86), block 17444928). The attack leverages the chain of vulnerabilities.   
- **22:59:01** — MANTRA attack \#2 ([tx 0x4956c7d9…](https://explorer.mantrachain.io/tx/0x4956c7d9919bd50602162885e8637fc6de6a9fd1d41321ebbb61875556deb1e5), block 17449159).  
- **23:13:01** — MANTRA halts ([block 17449398](https://explorer.mantrachain.io/block/17449398)), \~14 min after attack \#2.

**2026-08-21**

- **02:28:46** — MANTRA hotfix is released, [v0.6.0-v8-mantra-6](https://github.com/MANTRA-Chain/evm/releases/tag/v0.6.0-v8-mantra-6).  
- **03:36** – Secure email sent to individuals on the security contact list informing them of the critical, active exploit and providing remediation information.  
- **09:33:15** — Slack message sent to Cosmos EVM user group: Hi team, We strongly recommend all users to upgrade to following releases: v0.7.2 (https://github.com/cosmos/evm/releases/tag/v0.7.2) or v0.6.2 ([https://github.com/cosmos/evm/releases/tag/v0.6.2](https://github.com/cosmos/evm/releases/tag/v0.6.2)). Latest releases include critical security fixes.

**2026-08-22**

- **03:38:07** — MANTRA resumes on MANTRA chain `v8.4.0`  
- **19:46:37** — TAC attacked using the same chain of vulnerabilities used on MANTRA ([tx 0xae4e9b70…](https://explorer.tac.build/tx/0xae4e9b708ecef134a18aef8a1da9b4d24aa2a0e87f98d02695beae588cda46fc), height 24662148).  
- **19:46:37** — TAC exploitation: 2,985,651,403.40 TAC withdrawn from the *bonded\_tokens\_pool* ([tx 0xae4e9b70…](https://explorer.tac.build/tx/0xae4e9b708ecef134a18aef8a1da9b4d24aa2a0e87f98d02695beae588cda46fc), height 24662148).  
- **\~19:47** — Attacker bridges illicit TAC to BNB Chain via LayerZero OFT in two tranches: 500M ([tx 0xa0581dbd…](https://explorer.tac.build/tx/0xa0581dbdce6658055452f1903672803b9e599e843f550970a0491950e18987ec), height 24662168\) and 2.486B ([tx 0xce24d86f…](https://explorer.tac.build/tx/0xce24d86fb5f0962386927958b4317187652758f126f53e6022e37452d3a778e3), height 24662207); totaling \~2.986B TAC.  
- **19:47:37 / 19:48:28** — Bridged assets arrive on BNB Chain (deliveries: `0x00c739df…` block 117482626, `0xc5934bac…` block 117482738).  
- **19:49:34** — Liquidations begin on BNB Chain via KyberSwap (aggregator `0x6131b5fae1…`). The attacker sold consistently in small amounts while arbitrage bots traded against price differences in different venues to bypass the low liquidity in the public pool (e.g., [tx 0x6434dc46…](https://bscscan.com/tx/0x6434dc4670059c25838561117be8645e3f43477174e924b1f635c9a1752ec287), block 117482884). Approximately 1.2085B TAC is swapped for 950,293 USDT across \~80 transactions.  
- *Note: Secondary flows include 115M TAC bridged back to TAC (65.1M frozen by network halt) and 49.9M TAC bridged to TON, subsequently swapped on [STON.fi](http://STON.fi) for \~$55k. At the time of the post-mortem, \~1.662B TAC remains unsold on BNB Chain.*  
- **\~21:00–22:50**: KiiChain is exploited via the identified vulnerability ([tx 0xf45c07e9…](https://explorer.kiichain.io/tx/0xf45c07e94a4d4474220c96b1fff5f798bf22f4a4adf159d8f3e28c52caf1e840), block 9355102). Approximately 148.3M KII is withdrawn through 18 distinct exploit iterations. The perpetrator moves 67,597,997.87 KII to BNB Chain using the Hyperlane bridge protocol (address `0x0e7a9622…`). Roughly 80.7M KII (54.4% of total extracted) remains on KiiChain; these funds are recoverable following a network restoration. Asset liquidation on BNB Chain: The attacker swaps 64.6M KII for 1,607,323.41 USDT via PancakeSwap (BSC-USD/KII pool `0x238a3588…`). 3,000,000 KII is transferred to a KuCoin deposit address on BNB Chain.  
- **22:50:58** — KiiChain halts ([block 9355723](https://explorer.kiichain.io/block/9355723));  
- **23:45:25** — Further notices are sent on the secure email list and Cosmos EVM Slack user group to provide mitigation information and urge Cosmos EVM users to halt their blockchains immediately rather than perform coordinated governance upgrades, due to the ongoing attacks.   
- **23:58:11** — TAC halts ([block 24671475](https://explorer.tac.build/block/24671475)).

We are aware of three other chains that have been attacked using this same chain of vulnerabilities on or after this date, and we are not including their full details in this timeline for brevity, as the attack pattern is consistent. We continued providing mitigation information to affected chains throughout August 23, 24, and 25\. Please refer to the individual teams’ post-mortems for details on the attacks.

## Commitments

This exploit involved a set of chained vulnerabilities in Cosmos EVM, exploited by a sophisticated actor who attacked multiple chains over a short period.  Our dedicated cross-functional strike team worked continuously across global time zones over five days to understand the situation, provide mitigation information, and coordinate with affected users. We coordinated with 40 chains across this period. Cosmos Labs is committed to working internally and externally to improve the ecosystem’s security posture. 

Immediately, Cosmos Labs will make comprehensive changes to triage and remediation of critical vulnerabilities. This will involve developing more robust approaches for identifying cases where the vulnerability scope exceeds the scope documented in the original report, as in this case. Cosmos Labs will also increase awareness of security-critical CVD (coordinated vulnerability disclosure) channels across all Cosmos developer-facing properties, perform and optimize against regular health checks for developer responsiveness to these channels, and further define public standards for how and when these channels are used. At minimum, these standards will specify 1\) when network halts are recommended instead of coordinated upgrades and 2\) when private channels are used versus the public silent patch process.

Longer term, Cosmos Labs will perform a thorough audit of all operational security practices in partnership with security experts to identify additional opportunities to improve our security posture. 

Both of these initiatives will require collaboration with the broader ecosystem of open source contributors and users, given the scale and decentralized nature of the Cosmos Ecosystem. 

## Conclusion

This report discusses the situation holistically because teams running this software make operational decisions based on information provided in open source repositories. That obligation remains the same even when the situation is difficult, and those developers deserve an honest account of the events. 

We are grateful for the collaboration of the teams who were directly affected. They managed their own exploits and users, and still shared information with us quickly and in detail. Several had defenses and monitoring in place that limited the damage on their own networks, and we describe those measures in this post-mortem because they will help other teams in the ecosystem improve their security postures. We are also grateful to the security researchers who reported the underlying issues through the bug bounty program and continued to engage with us during the response. 

Cosmos Labs remains committed to strengthening the security of our software, vulnerability management processes, and disclosure practices. You can find Cosmos EVM security [disclosures](https://github.com/cosmos/evm/security/advisories) on GitHub and the latest information on [supported releases](https://docs.cosmos.network/sdk/latest/release-family) in the developer documentation. Teams that use the Cosmos stack and would like to receive private security notifications can fill out [this form](https://docs.google.com/forms/d/e/1FAIpQLSccECADTobFqRa1Z4T9xtlIY4w4AalnvEwheBk60e515QUP7w/viewform) and email [security@cosmoslabs.io](mailto:security@cosmoslabs.io) to complete KYC. In addition to Cosmos developers, we invite security personnel from major bridges, exchanges, and offramps to join, since these providers are in the critical path of fund withdrawal. We welcome security researchers to engage with us through our [bug bounty program on Immunefi](https://immunefi.com/bug-bounty/cosmos/information/). 

—

This report is provided for informational purposes only and does not constitute an admission of liability. The Cosmos technologies are free, open-source software provided under their respective license terms without warranty of any kind. Nothing in this report creates, expands, or modifies any legal duty or obligation beyond those set out in the applicable open-source licenses.  
