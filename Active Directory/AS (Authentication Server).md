---
tags:
  - AD
date: 2023-09-1
---
- Part of the [[Kerberos]] authentication protocol, located within the [[KDC (Key Distribution Center)]].
- Responsible for verifying the user's credentials during initial authentication.
- Issues [[Ticket Granting Tickets (TGTs)]].
- First step in Kerberos authentication - validates the user but not the service they want to access.
# Attacks

- [[AS-REP Roasting]] abuses users not requiring pre-authentication by capturing AS responses from here. Read more above.