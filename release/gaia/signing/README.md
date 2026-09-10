# Gaia Release Signature Verification

Use the public key below to verify detached signatures accompanying Gaia releases.

- **Signing identity:** Cosmos-Release <nodes@cosmoslabs.io>
- **Public key:** [cosmos-release.asc](keys/cosmos-release.asc)
- **Fingerprint:** `E625 9F16 9C7B 913D BB75 DE02 5395 305D 29B8 8B32`

## Verify the public key fingerprint

Download the public key and inspect its fingerprint:

```bash
curl --fail --location --output cosmos-release.asc \
  https://raw.githubusercontent.com/cosmos/security/main/release/gaia/signing/keys/cosmos-release.asc

gpg --show-keys --with-fingerprint cosmos-release.asc
```

Confirm that the full primary key fingerprint matches the value above before continuing.

## Verify a release

Place the release archive and its detached signature in the current directory. For example, for `gaiad-linux-amd64.tar.gz` and `gaiad-linux-amd64.tar.gz.asc`, run:

```bash
gpg --import cosmos-release.asc
gpg --verify gaiad-linux-amd64.tar.gz.asc ./gaiad-linux-amd64.tar.gz
```

Successful verification includes output similar to the following, with the signature timestamp and local trust label shown as placeholders:

```text
gpg: Signature made <signature date and time>
gpg:                using EDDSA key E6259F169C7B913DBB75DE025395305D29B88B32
gpg: Good signature from "Cosmos-Release <nodes@cosmoslabs.io>" [<trust label>]
```

- `<signature date and time>` is when the signature was created, displayed using your local date/time settings; it varies by release.
- The fingerprint after `using EDDSA key` must match the full fingerprint above (ignoring spaces).
- `<trust label>` depends on GPG's local trust settings and may be `unknown`, `full`, or `ultimate`. It does not need to be `ultimate` for signature verification to succeed.

Only extract and use the release archive if verification reports `Good signature` from the key identified above. If verification fails, the signer does not match, or GPG reports an expired or revoked key, do not extract the archive or run its contents.

After importing the public key, you may see `[unknown]` and the following warning even when GPG reports `Good signature`:

```text
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: E625 9F16 9C7B 913D BB75  DE02 5395 305D 29B8 8B32
```

This means that GPG has not established the key owner's identity through your local trust settings. The warning alone does not mean that the archive was modified or that signature verification failed.

**You may proceed despite this specific warning if verification succeeds with `Good signature` and the signer's full fingerprint matches the fingerprint above, confirmed from the official project repository.** The failure conditions above still apply. You do not need to create a personal GPG key or set this release key's trust level to `ultimate` to verify the release.

For more detail, see [GnuPG's explanation of this warning](https://gnupg.org/download/integrity_check.html).

## Scope

This signing key is used for all Gaia releases, including regular and emergency releases.

Signatures verify the release signing key and archive integrity. They do not guarantee that the included binary is vulnerability-free or functions correctly.

For emergency patches, binaries and signature files are distributed through the existing private channels.
