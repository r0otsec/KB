---
tags:
  - AD
  - knowledge
date: 2023-09-1
---
- Core AD database file.
- Stores all domain information:
	- users
	- groups
	- password hashes
	- [[GPO (Group Policy Object)|GPOs]]
- Located at:
	- `C:\Windows\NTDS\NTDS.dit`
# Security

- Contains entire domain's credentials.
- NTLM, LM (if enabled) and [[Kerberos]] secrets stored in encrypted form.
- Access requires DC privileges.
- Backed by SYSTEM registry hive for boot key.