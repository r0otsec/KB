---
tags:
  - knowledge
  - windows
date: 2023-09-1
---
- Technique
- Attackers add alternate credentials to AD account (computer/service) to allow unauthorized [[Kerberos]] authentication without changing actual password/key.
- Works only if Certificate-Based Logon (PKINIT) is supported.
# How It Works

- Attacker abuses write access to target AD object (computer account).
- Write a `msDS-KeyCredentialLink` attribute, which:
	- stores a certificate mapping.
	- is used for Kerberos [[PKINIT authentication]].
- Attacker can authenticate via Kerberos with private key, without [[NTLM]]/Kerberos password hash.
# Usage

1. Generate a key pair and a self-signed cert.
2. Add forged KeyCredential to the target object's `msDS-KeyCredentialLink`
3. Authenticate using `PKINIT` (e.g. via `Rubeus` or `ForgeCert`)
# Tools

- Common tools for exploitation include `Whisker`, `ForgeCert`, `Rubeus` and `Certipy`.
# Detection/Defense

- Look for changes to `msDS-KeyCredentialLink` attribute.
- KeyCredential blobs are non-human-readable, but changes to it are rare.
- Audit Event ID `5136`.
- Limit who can write to computer accounts.
#