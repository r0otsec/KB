---
tags:
  - AD
date: 2023-09-1
---
- [[AS (Authentication Server)]] request in Kerberos.
- Sent by client to the AS (part of the [[KDC (Key Distribution Center)|KDC]]).
- Triggers the start of the Kerberos login process.
- If valid/pre-auth enabled, AS responds with [[AS-REP (Authentication Service Response)|AS-REP]] containing [[Ticket Granting Tickets (TGTs)|TGT]]
# Contents

Typically contains:

- Client principal name (username).
- Timestamp encrypted with user key (derived from password) - used for pre-auth.
- Realm (domain).
- Target server (TGS).
# Attacks

- Part of [[AS-REP Roasting]] attack.
- Exploits accounts that do not require pre-authentication.
- If pre-auth is disabled, can send AS-REQs without knowing password.

