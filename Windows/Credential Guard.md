- Security feature.
- Uses virtualization-based security (VBS) to isolate/protect [[LSASS (Local Security Authority Subsystem Service)|LSASS]] memory from access.
- Introduced in Windows 10 Enterprise/Server 2016.
# How It Works

- LSASS no longer stores sensitive credentials in normal process memory.
- Offloads credential secrets to secure, isolated memory space.
- Prevents most tools from accessing credentials directly.
# Protections

- Typically blocks:
	- `Mimikatz`
	- LSASS dumping
	- Offline analysis with `Prodcump`, `Pypykatz`, etc..
- Protects:
	- [[NTLM]] hashes.
	- [[Kerberos Tickets]]
	- [[WDIGEST]] and SSP plaintext creds.
# Limitations

- Does not stop:
	- [[Pass The Hash]]
	- Keylogging or grabbing creds at input.
	- Abusing stored credentials (e.g. Credential Manager).
	- Credential theft from non-LSASS sources.
- Can be disabled with boot-level access or GPO changes if not hardened.
# Detection

- Check status via:
	- `Get-CimInstance -ClassName Win32_DeviceGuard`
	- Look for CredentialGuard = Running
- Enforce via:
	- Group Policy -> Device Guard > Credential Guard
	- Secure Boot, virtualization support required.

