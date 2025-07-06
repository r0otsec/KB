---
tags:
  - AD
date: 2023-09-1
---
- Response from the [[AS (Authentication Server)|AS]] within the [[KDC (Key Distribution Center)|KDC]] during [[Kerberos]] authentication.
- Sent after validating a user's creds.
- Decrypted by client to access TGT and establish session with [[Ticket Granting Service (TGS)|TGS]].
- Only sent after successful authentication and time validation.
# Contents

It contains:

- [[Ticket Granting Tickets (TGTs)|TGT]], encrypted with the TGS secret key.
- Session key, encrypted with users key (derived from password).
# Attacks

- Part of [[AS-REP Roasting]] attack
- Exploits accounts that do not require pre-authentication.
