---
tags:
  - AD
date: 2023-09-1
---
- Type of managed service account introduced in Server 2012.
- Allows services on multiple machines to use same account
	- automated password management.
# Purpose

- Securely run services, scheduled tasks, or apps without hardcoded creds.
- Active Directory handles:
	- Password complexity
	- Periodic automatic rotation
		- automatically every 30 days
	- Access control to who can retrieve the password.
# Characteristics

- Managed by `Key Distribution Service (KDS)`.
- Passwords are complex, long and rotated automatically.
# Deployment

- Created with PowerShell:
	- `New-ADServiceAccount -Name gmsaWebApp -DNSHostName web.domain.local -PrincipalsAllowedToRetrieveManagedPassword "WebServers"`
- Installed on machines:
	- `Install-ADServiceAccount -Identity gmsaWebApp`
- Used in service config as:
	- `DOMAIN\gmsaWebApp$`
# Attacks

- If attacker has LocalSystem/SYSTEM access, extraction can be done via `DSInternals`, `Mimikatz` or `SharpGMSA`.
- Common abuse scenarios:
	- Dump gMSA password and use to move laterally.
	- Look for overly broad PrincipalsAllowedToRetrieveManagedPassword.
- gMSAs can have SPNs - candidates for [[Kerberoasting]].