---
tags:
  - windows
date: 2023-09-1
---
- Core Windows subsystem.
- Handles security policy, user auth, access tokens and auditing.
- Implement as the process:
	- `lsass.exe` - (Local Security Authority Subsystem Service).
- Typically located at:
	- `HKLM\SECURITY\Policy\Secrets`
# LSA Secrets

- Sensitive system values stored by LSA in registry.
- Often include cached creds, service account passwords, DPAPI keys.
- - Encrypted with a system key derived from boot key and stored under:
	- `HKLM\SYSTEM`
# Responsibilities

- Verifies user logons (local/domain).
- Manages:
	- access tokens
	- credential storage ([[NTLM]] hashes, [[Kerberos]] tickets, plaintext creds via [[SSPs]] like [[WDIGEST]]).
	- local security policy.
	- audit logging and system security events.
- Communicates with:
	- AD (for domain auth).
	- [[SAM]] (local account database).
	- Cred providers/security packages.
# Security

- Runs as protected process (`lsass.exe`).
- Starts at boot with `SYSTEM` privileges.
- Interacts heavily with:
	- [[LSASS (Local Security Authority Subsystem Service)|LSASS]] memory.
	- [[SSPs]].
	- [[DPAPI]] (for encryption/decryption of secrets).
- Common dumping tools include:
	- `mimikatz` -> `sekurlsa::logonpasswords`
	- `Procdump` + `Pypykatz`
	- `comsvcs.dll` (abuses rundll32).
- Techniques include:
	- LSASS dumping (offline/live).
	- Injecting malicious SSPs or DLLs.
	- Using `SeDebugPrivilege` or `SeTcbPrivilege` to read memory.
# Defenses

- [[Credential Guard]] can isolate LSA secrets in protected VBS space.
- Use Protected Process Light (PPL) to restrict LSASS access.
- Monitor:
	- suspicious access to `lsass.exe`
	- use of `SeDebugPrivilege`
	- tools writing minidumps (Event IDs 10, 4697, 7045, 11/Sysmon).
# Notes

- For domain systems, LSA interacts with the [[KDC (Key Distribution Center)|KDC]] for Kerberos operations.
- LSA manages SSPI.
- Compromising LSA = total access to current user sessions/cached creds.


