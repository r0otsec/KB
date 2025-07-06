---
tags:
  - knowledge
  - AD
  - windows
date: 2023-09-1
---
 - Used to centrally manage settings and enforce policies across domain-joined machines and users.
 - Controls security settings, software deployment, startup scripts, user restrictions.
# Structure

- GPOs are linked to:
	- sites
	- domains
	- organizational units (OUs)
- Types of policies include:
	- `Computer configuration`: applied at machine startup, affects system-wide settings.
	- `User configuration`: applied at logon, affects user environment.
- There is a precedence order for GPOs:
	- 1. Local
	- 2. Site
	- 3. Domain
	- 4. OU (nested OUs processed from parent to child)
# Files

- GPO files are stored under:
	- `\\<DOMAIN>\SYSVOL\<DOMAIN>\Policies\{GUID}`
- Registry settings applied via:
	- `HKLM\Sofware\Policies\..` for computer config
	- `HKCU\Software\Policies\..` for user config
# Security

- GPO application depends on Read + Apply Group Policy permissions.
- Can delegate GPO creation, editing, or linking privileges via Group Policy Management Console (GPMC).
- Authenticated users typically have read + apply permissions by default.


