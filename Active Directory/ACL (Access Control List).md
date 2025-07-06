---
tags:
  - knowledge
  - AD
date: 2023-09-1
---

- Contains list of elements ([[ACE (Access Control Entries)|ACEs]]).
- Each entry contains trustee and defines type of access trusted has for object in question.
	- Trustee may be things like users, groups or login sessions.
# Types of ACLs

- Discretionary Access Control List (DACL)
	- defines access rights of trustee to object.
	- contains allow/deny ACEs
- System Access Control List (SACL)
	- generate audit logs specifying if a trustee was trying to access an object.
	- specifies if successful or not and what access was granted.
	- contain system audit ACEs.

# Enumeration

- [[BloodHound]]
	- maps relationships between objects.
	- quickly identifies possible paths.
	-  Check "Outbound/Inbound Object Control".
	- `bloodhound-python -u 'user' -p 'password' -d test.local -c All -dc dc01.test.local -ns 192.168.100.1`.
- [[ADACLScanner]]
	- PowerShell script.
	- Audits ACLs (DACLs & SACLs).
- PowerShell
	- `(Get-Acl "AD:$(Get-ADGroup DBOWNERS)").Access  | Select-Object ActiveDirectoryRights,IdentityReference,AccessControlType | Select-String lares`.

# Abusing ACLs

- GenericAll
	- all possible access rights.
	- Permission value - `ADS_RIGHT_GENERIC_ALL`.
- GenericWrite
	- permission to write all properties of object.
	- Permission value - `GENERIC_WRITE`.
	- objectType can contain GUID identifying a set/property.
		- if not, ACE controls right to write all object's properties.
- WriteProperty
	- permission to write over specific attributes.
	- Permission value - `ADS_RIGHT_DS_WRITE_PROP`
	- Over computers:
		- [[Shadow Credentials]]
		- [[Resource Based Delegation|RBCD]]
		- [[SPN Jacking]]
	- Over users:
		- Shadow Credentials
		- [[Kerberoasting]]
		- Logon Script
	- Over groups:
		- AddMember
- WriteDacl
	- modify DACL in object security descriptor.
	- Permission value - `ADS_RIGHT_WRITE_DAC`.
- WriteOwner
	- assume ownership of the object.
	- Permission value - `ADS_RIGHT_WRITE_OWNER`
- Self (Self-Membership)
	- validated write permissions to update group membership regarding adding/removing account.
	- Rights-GUID - `bf9679c0-0de6-11d0-a285-00aa003049e2`
- AllExtendedRights
	- perform operations controlled by extended access right.
	- allows resetting passwords on user objects
	- allows crafting RBCD attacks for computers
	- Permission value - `ADS_RIGHT_DS_CONTROL_ACCESS`
	- Over group:
		- AddMember
	- Over user:
		- ForceChangePassword
	- Over computer:
		- ReadLAPSPassword
- ReadLAPSPassword
	- right to read `ms-mcs-admpwd` attribute for computer with [[Local Administrator Password Solution (LAPS)|LAPS]].
- ForceChangePassword
	- right to reset password for user.
	- Rights GUID - `00299570-246d-11d0-a768-00aa006e0529`.

# Detections

Use Event Logs, Sysmon and AD audit policies to identify abuse of specific ACL rights. A list of event IDs include:

- WriteDACL/WriteOwner
	- Monitor changes to `nTSecurityDescriptor` via Event ID 5136 (Directory Service Changes)
- GenericAll/GenericWrite/WriteProperty
	- Check unexpected modifications to objects using 5136.
	- HVTs include `servicePrincipalName`, `msDS-AllowedToActOnBehalfOfOtherIdentity`, `member`.
- ForceChangePassword
	- Check for event ID 4724 (attempt to reset account pass).
- ReadLAPSPassword
	- Audit access to `ms-MCS-AdmPwd` attribute.
	- Configure alerts for non-priv user requests.
- BloodHound
	- Detect LDAP queries with unusual volume or sensitive object targeting.
