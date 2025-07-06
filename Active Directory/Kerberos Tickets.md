---
tags:
  - AD
  - windows
date: 2023-09-1
---
- [[Kerberos]] uses encrypted tickets to authenticate users/services.
# Ticket Types

- [[Ticket Granting Tickets (TGTs)]]:
	- issued by [[KDC (Key Distribution Center)]] at logon
	- proves identity.
	- used to request access to services.
	- encrypted with `krbtgt` account key.
	- cached locally.
- [[Ticket Granting Service (TGS)]]:
	- issued by the KDC when accessing a service.
	- proves identity to specific service.
	- encrypted with service account key.
	- can be requested multiple times with same TGT.
# Storage

- Stored in memory (e.g. `klist`, `mimikatz`, `rubeus`).
- Tickets cached by [[LSASS (Local Security Authority Subsystem Service)]].
- `C:\Windows\Temp\krb55cc_*` - if using MIT Kerberos.