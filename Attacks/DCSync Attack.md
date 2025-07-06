---
tags:
  - knowledge
  - AD
  - attack
date: 2023-09-1
---
- Post-exploitation attack
- Attacker impersonates a [[Domain Controller]] to request replication of password data.
	- includes [[NTLM]] hashes, [[Kerberos]] keys, and `krbtgt` secrets.
- Abuses replication permissions reserved for DCs.
- Extracts user creds from AD without touching [[LSASS (Local Security Authority Subsystem Service)|LSASS]] or target system.
# Background

- AD replication keeps DCs in sync via `DRSUAPI RPC` interface.
- Function `DRSGetNCChanges()` lets DC request changes from another including:
	- NTLM hashes
	- AES keys
	- LM hashes
	- KRBTGT account
# Requirements

- Need account with following directory-level permissions on domain root object:
	- `Replicating Directory Changes`
	- `Replicating Directory Changes All`
	- `Replicating Directory Changes In Filtered Set` (optional)
- Permissions usually held by:
	- `Domain Controllers`
	- `Domain Admins`
	- `Enterprise Admins`
	- Any user granted them manually or via ACL abuse (e.g. [[BloodHound]] path like `GetChangesAll`).
# Tools

- Linux (Impacket):
	- dumping all hashes:
		- `secretsdump.py -just-dc CORP/user:pass@dc.corp.local`
	- dump a specific user:
		- `secretsdump.py -just-dc-user krbtgt CORP/user:pass@dc.corp.local`
	- dump with NTLM hash:
		- `secretsdump.py -just-dc -hashes :<NTLM> CORP/user@dc`
- Windows (mimikatz):
	- dump domain admin hash:
		- `lsadump::dcsync /domain:corp.local /user:Administrator`
	- dump krbtgt:
		- `lsadump::dcsync /domain:corp.local /user:krbtgt`
# Use Cases

- Extracting NTLM hashes for all domain users.
- Dumping krbtgt hash for [[Golden Ticket Attack]].
- Cred theft without touching LSASS.
# Detection

- No LSASS access - endpoint AV may miss it.
- Monitor:
	- `Event ID 4662` (object access - look for `DS-Replication-Get-Changes`)
	- `Event ID 5136` (ACLs modified to grant replication rights)
	- DRS replication API calls from non-DC host.
# Mitigation

- Audit ACLs on domain root object for replication rights:
	- `Get-ACL "AD:\DC=corp,DC=local"`
- Remove replication permissions from users/groups that don't require them.
- Monitor for replication protocol use from non-DCs.
- Rotate krbtgt password twice if compromise is suspected.
# Notes

- One of the stealthiest post-exploitation techniques.
- Does not require foothold on a DC.
- Often used to:
	- perform `Golden Ticket` attacks.
	- maintain persistence.
	- dump full cred database.

