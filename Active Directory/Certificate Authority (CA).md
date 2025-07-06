---
tags:
  - AD
  - knowledge
date: 2023-09-1
---
- Core component of [[ADCS (Active Directory Certificate Services)|ADCS]].
- Issues and signs digital certs for identity, encryption and authentication.
- Certificates bind public key to user, computer or service.
- Located under `Server Manager` -> `Certification Authority`
	- Includes revoked and issued certs.
# Types

- Enterprise CA
	- integrated with AD.
	- publishes templates and certs to domain-joined objects.
	- uses certificate templates for automated enrollment.
- Standalone CA
	- not integrated with AD.
	- manual cert requests and approvals.
# Attacks

- Weak CA configs/misused templates.
- Common abuses:
	- requesting certs that can be used for authentication.
