---
tags:
  - knowledge
  - attack
  - linux
date: 2023-09-1
---
- Legacy [[Kerberos]] delegation setting.
- Service/computer trusted to impersonate users to `ANY` service.
# How It Works

- User authenticates to a system.
- [[Ticket Granting Tickets (TGTs)|TGT]] cached in memory [[LSASS (Local Security Authority Subsystem Service)|LSASS]].
- System can then reuse the TGT to access other services as the user.
- Set via:
	- Account property - `TrustedForDelegation = TRUE`.
	- Group Policy - `Trust this computer for delegation to any service (Kerberos only)`.
# Attacks

- TGT Extraction - attackers extract TGTs of any users who log in.
- Abuse cases:
	- Dump TGT from LSASS using:
		- `mimikatz sekurlsa::tickets`
		- `Rubeus dump`
	- Relay auth to unconstrained host using printer bug or SMB relays, then extract TGT.
# Detection & Enumeration

- PowerView:
	- `Get-DomainComputer -Unconstrained`
- LDAP filter:
	- `(userAccountControl:1.2.840.113556.1.4.803:=524288)`
- Look for:
	- `TRUSTED_FOR_DELEGATION` flag in `userAccountControl`
	- TGT presence in LSASS memory on non-DC systems.
# Notes

- Considered insecure and deprecated.
- Often replaced with:
	- [[Constrained Delegation]]
	- [[Resource Based Delegation]]

