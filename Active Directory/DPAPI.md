---
tags:
  - AD
  - windows
  - knowledge
date: 2023-09-1
---
- Windows built-in system for encrypting/decrypting sensitive data.
- Used by apps/Windows to protect things like:
	- Browser creds.
	- WiFi keys.
	- Stored passwords.
	- [[Credential Manager]] secrets.
- Tied to the user's password or machine creds.
# Process

- When data is protected:
	- DPAPI encrypts using key derived from user's password hash.
	- Encrypted data only decrypted by same user/account on same system or with proper keys.

- On machines inside [[Active Directory]]:
	- Backup keys created and stored in AD (`ms-DS-Password-Settings`) or through DPAPI domain backup key.
		- Allows domain admins to recover DPAPI-encrypted data.
		- Only generated once during domain creation.
# Location

- Usually located under:
	- `C:\Users\$USER\AppData\Roaming\Microsoft\Protect\$SUID\$GUID`
- Common paths of hidden files include:
	- `C:\Users\$USER\AppData\Local\Microsoft\Credentials\`
	- `C:\Users\$USER\AppData\Roaming\Microsoft\Credentials`
# Attacks

- Tools like `mimikatz`, `DPAPIDump`, `dpapi.py`, `SharpDPAPI` or `Rubeus` can:
	- Extract DPAPI master keys.
	- Decrypt creds.
	- Abuse domain backup keys.

