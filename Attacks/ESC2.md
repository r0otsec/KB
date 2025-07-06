---
tags:
  - attack
  - knowledge
  - AD
  - windows
  - redteam
date: 2023-09-1
---
- [[ADCS (Active Directory Certificate Services)|AD CS]] misconfiguration.
- [[Certificate Template]] allows user to spoof the subject name field without needing to abuse the SAN field.
- Similiar to [[ESC1]] but no need to mess with SANs.
# Background

- Certificate templates usually define how the subject name is set:
	- from AD (safe).
		- uses requester's own name.
	- supply in the request (dangerous).
		- requester tells the CA `"Hey, this cert is for Administrator"`.
- If `Supply in the Request` is enabled, attacker can set the subject name to anyone.
- Mostly a legacy compatibility path.
- When a cert has:
	- spoofed Common Name (CN) or Subject Name
	- AND the `Client Authentication` EKU.
- AD will trust it during [[PKINIT authentication]] since:
	- [[Kerberos]] falls back to matching against Subject Name if SAN not present.
	- AD does not check if requester is person in Subject Name.
- The same effect as ESC1:

>[!danger]
>Auth as Administrator, without touching the SAN field.
# Vulnerable Template Criteria

- Templates vulnerable to ESC2 if:
	- Subject Name is set to `Supply in the request`.
	- Has the Client Authentication EKU.
	- You have `Enroll` permissions.
	- The CA is issuing from the template.
- Typically found in legacy v1 templates created on old systems but still common.
#  Exploitation

- Find the vulnerable template:
	- `certipy-ad find -u user@corp.local -p 'Password123!' -dc-ip 10.0.0.5 -vulnerable`
	- Look for:
		- Template with SubjectName = Supply in the request.
		- EKU = `Client Authentication`.
		- Enroll permissions granted.
- Request cert with spoofed subject name:
	- `certipy-ad req -u user@corp.local -p 'Password123!' -ca corp-CA -template LegacyTemplate -subject "CN=Administrator -dc-ip 10.0.0.5 -output esc2" `
		- no need to use `-upn` or spoof the SAN.
- Authenticate using the cert:
	- `certipy-ad auth -pfx esc2.pfx -dc-ip 10.0.0.5`
	- `gettgtpkinit.py -pfx esc2.pfx corp.local/Administrator`

# Detection & Logging

- `Event ID 4886` (certificate issued).
- Check for mismatch between certificate SAN and requester.
- `Event ID 4768` (Kerberos AS-REQ).
- Look for:
	- templates allowing "supply in request".
	- certificate subjects not matching requester identities.
# Mitigation

- Don't use `Supply in request` for Subject Name - use `Build from Active Directory`.
- Audit templates:
	- `Get-CATemplate | Where-Object {$_.SubjectNameFlag -match "EnrolleeSupply"}`.
- Restrict enroll permissions.
- Enable manager approval for any legacy templates.