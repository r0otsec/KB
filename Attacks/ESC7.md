---
tags:
  - attack
  - knowledge
  - AD
  - windows
  - redteam
date: 2023-09-1
---
- Privilege escalation path.
	- low priv user can coerce a [[Certificate Authority (CA)|CA]] to issue a cert for privileged user.
- CA has `EDITF_ATTRIBUTESUBJECTALTNAME2` enabled.
- Attacker has write permissions to the CA object in AD.
- Allows attacker to abuse config to request certs with arbitrary SAN:
	- e.g. UPN of a domain admin & authenticate via [[PKINIT authentication|PKINIT]].
# Background

- `EDITF_ATTRIBUTESUBJECTALTNAME2` is a CA flag that allows certificate requesters to specify SANs inside their CSR.
- Normally disabled to prevent identity spoofing.
- If CA permits and attacker has write access to its AD object:
	- attackers can abuse the setting to impersonate other users.
# Vulnerability Criteria

- Vulnerable if:
	- CA security descriptor allows the attacker:
		- `ManageCA` or `ManageCertificate` permissions (typically via `WriteDACL` or `GenericAll`).
	- CA has `EDITF_ATTRIBUTESUBJECTALTNAME2` enabled.
	- Attacker has enrollment rights on any cert template with valid EKUs.