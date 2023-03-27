### Example Timeline

The following is an example timeline for the triage and response.

The required roles and team members are described in parentheses after each task; however, multiple people can play each role and each person may play multiple roles.

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

