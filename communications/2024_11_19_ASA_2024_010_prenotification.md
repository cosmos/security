ASA-2024-010: cosmossdk.io/math: Pre-notification for upcoming High severity patch

A patch for a High severity issue affecting the cosmossdk.io/math package versions < v1.4.0 will be released on November 20th, 2024 at 16:00 GMT at the Cosmos SDK repository. This patch addresses a potential liveness issue that may impact most networks.

This issue impacts consumers of the cosmossdk.io/math, which includes popular modules including IBC-Go and tokenfactory. If your chain interacts with APIs in the cosmossdk.io/math package, or utilizes a module that consumes this library, it is advised to update to the latest version at the time of the patch release by updating your project's go.mod dependency for cosmossdk.io/math

The patch can be applied without a hard-fork, and with a version bump in a chain's go.mod fie.

You are receiving this email because you either signed up for Security Notifications. A copy of this notification can be found at the /security repository.
