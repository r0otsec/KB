---
tags:
  - knowledge
  - windows
  - AD
date: 2023-09-1
---
- Form of [[Kerberos Delegation]].
- Target service controls who is allowed to impersonate users to it.
- Introduced in Server 2012.
# How It Works

- Configured via the `msDS-AllowedToActOnBehalfOfOtherIdentity` attribute on the target service account.
- Attribute contains an [[ACL (Access Control List)|ACL]] of security principals (computers/accounts) that are allowed to delegate to the service.
- Supports S4U2Self + S4U2Proxy behind the scenes to impersonate users.
# Attacks

- Can be abused without elevated privileges.
- Does not require Domain Admin if ACL is misconfigured.
- Common attack chain:
	- create new computer account (or compromised one).
	- set [[Security Identifier (SID)|SID]] in the `msDS-AllowedToActOnBehalfOfOtherIdentity` of a target service account.
	- Use S4U2Self or S4U2Proxy to impersonate a domain user.
# Detection/Defense

- Monitor for changes to `msDS-AllowedToActOnBehalfOfOtherIdentity`.
- Restrict who can create/join computers to the domain.
- Avoid granting write access to service accounts.
- Look for abuse via Event Logs:
	- Event ID 4769 (TGS requests), especially with `Service Name` not matching user identity.
- For quick checks, view delegation ACLs:
	- `Get-ADComputer TargetComputer -Properties 'msDS-AllowedToActOnBehalfOfOtherIdentity'`.

