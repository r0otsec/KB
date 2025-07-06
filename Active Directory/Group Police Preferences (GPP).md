---
tags:
  - AD
date: 2023-09-1
---
- Set of extensions to Group Policy.
- Allows admins to configure settings without writing scripts.
- Simplifies deployment of non-security settings.
- Gets processed by client machines like regular [[GPO (Group Policy Object)|GPOs]].
# Use Cases

- Map network drives/printers.
- Set registry values.
- Create local users/groups.
- Configure services, environment variables, and scheduled tasks.
- Set IE/Windows settings without custom ADM templates.
# Attacks

- GPP could store passwords in SYSVOL using weak AES. Stored in XML files under:
	- `Groups.xml`
	- `Services.xml`
	- `Scheduledtasks.xml`
	- `DataSources.xml`
- Tools can extract/decrypt passwords from files using `gpp-decrypt`, `Get-GPPPassword` or `Metasploit`.
# Locations

- For locations, the SYSVOL share on DCs:
	- `\\DOMAIN\SYSVOL\DOMAIN\Policies\`
- To search for files:
	- `findstr /S /I cpassword \\DC\SYSVOL\DOMAIN\Policies\*.xml`
- Look for:
	- `cpassword=` in XML
	- XML files in `Machine\Preferences\Groups`, `ScheduledTasks`, or `Services`.
# Update

- Microsoft disabled the password feature in 2014, but legacy GPP XMLs can still exist.
- GPP can still deploy commands or scheduled tasks.

