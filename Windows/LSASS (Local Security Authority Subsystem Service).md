---
tags:
  - windows
date: 2023-09-1
---
- `lsass.exe` - core Windows process.
- Handles auth, cred management, local security policies.
- Process behind the [[LSA (Local Security Authority)]].
# Responsibilities

- Verifies user creds during logon.
- Generates access tokens.
- Manages:
	- [[Kerberos]] and [[NTLM]] authentication.
	- [[DPAPI]], [[SSPI]], and [[SSPs]] (e.g. [[WDIGEST]], [[MSV]])
	- Cached logon data
	- LSA secrets
# Security

- Runs as `SYSTEM` with elevated privileges.
- Process located under:
	- `C:\Windows\System32\lsass.exe`
- Modern Windows runs as a `Protected Process Light (PPL)` to prevent tampering.
- Contains all active session creds in memory.
# Defenses

- Enable [[Credential Guard]].
- Enforce LSASS protection (`RunAsPPL`):
	- `New-ItemProperty -Path "HKLM\SYSTEM\CurrentControlSet\Control\Lsa" -Name "RunAsPPL" -Value 1 -PropertyType DWORD -Force`
- Monitor:
	- Event IDs `10`, `11`, `4697` and `7045`.
	- Unusual processes accessing LSASS.
	- Use of `SeDebugPrivilege` or `rundll32`, `procdump`, etc..
# Notes

- LSASS $\neq$ LSA secrets.
- Dumped creds can be reused for:
	- [[Pass The Hash]]
	- [[Pass the Ticket]]
	- [[Overpass the Hash]]
	- [[Silver Ticket Attack]]
	- [[Golden Ticket Attack]]

