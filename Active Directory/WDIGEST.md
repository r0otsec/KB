---
tags:
  - AD
  - windows
  - knowledge
date: 2023-09-1
---
- Legacy Windows authentication protocol.
- Supports HTTP-based single sign-on using username/password in plaintext.
# How It Works

- Used for digest authentication in services like:
	- IIS (web servers).
	- HTTP-based proxy/auth challenges.
	- Some legacy remote management tools.
- Credentials (username/password) stored in [[LSASS (Local Security Authority Subsystem Service)|LSASS]] memory in plaintext when enabled.
# Attacks

- WDigest allows:
	- plaintext password extraction from memory (LSASS).
	- no need for NTLM cracking.
- Tools used include:
	- `mimikatz sekurlsa::logonpasswords`
	- `Procdump` + `Pypykatz`
# Enabling/Disabling

- Since Windows 8.1/Server 2012 R2, WDigest is disabled by default.
- Controlled via registry key:
	- `HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest`
		- `UseLogonCredential = 1 (enabled - insecure)`
		- `UseLogonCredential = 0 (default)`
# Notes

- Still found enabled in some environments for compatibility.
- [[Credential Guard]], if enabled, protects against attacks.
- Use `mimikatz logonpasswords` to check if storing in plaintext.