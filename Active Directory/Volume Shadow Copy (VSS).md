---
tags:
  - AD
  - windows
  - knowledge
date: 2023-09-1
---
- Allows creation of point-in-time snapshots of disk volumes.
- Used for backups and restoring files.
# Purpose

- Enables file and volume level backups without locking files.
- System restore points.
- Forensic snapshots or rollback after failed updates.
# Typical Snapshot Targets

- AD DB - `C:\Windows\NTDS\NTDS.dit`
- Registry hives - `C:\Windows\System32\config\SYSTEM`, `SAM`, `SECURITY`.
- Event logs, system files, user data.
# Attacks

- Allows offline extraction of sensitive files.
- Common toolchains:
	- Use `vssadmin`, `diskshadow` or `PowerShell` to create/expose a shadow copy.
	- Copy [[NTDS.dit]] and SYSTEM hive for hash extraction.
	- Dump creds with:
		- [[Secretsdump]]
		- [[Mimikatz]]
		- [[Impacket Toolkit|Impacket]]
- Example flow includes:
	- `vssadmin create shadow /for=C:`
	- `copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\NTDS\ntds.dit .`
	- `copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SYSTEM .`
# Detection

- Suspicious use of:
	- vssadmin
	- wmic shadowcopy
	- diskshadow
- Unusual reads from `GLOBALROOT\Device\HarddiskVolumeShadowCopyX`
- Monitor for Event IDs:
	- `2001` (VSS snapshot created)
	- `2003` (VSS snapshot deleted)
# Notes

- Requires Administrator/SYSTEM privileges.
- Common in post-exploitation stages.
- VSS can be disabled via policy.
- Disk usage limits may remove old shadow copies automatically.

