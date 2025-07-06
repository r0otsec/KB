---
tags:
  - knowledge
  - AD
date: 2023-09-1
---
- Provides PKI within [[Active Directory]] for management and issuing of digital certificates.
- Uses a [[Certificate Authority (CA)]] to issue and manage X.509 certs.
	- used for secure comms and identity verification.
- Integrates with Group Policy to issue/manage certs for domain-joined machines.
- Provides ability for users to easily request certs and/or automate PKI processes.
# CA Roles

- Root CA - primary authority issuing certs
- Subordinate CA - issued by root, manages cert request process.
- Online CA - issues certs in real time to clients (user/machine certs).
- Offline CA - used for secure key signing, kept isolated.
# Cert Templates

- CA issues certs according to settings specified by objects.
- Templates use enrolment policies/predefined configs to dictate validity period, usage, request permissions and other parameters.
- Issued certs used for domain authentication.
	- Certs can be mapped to AD accounts.
- Comes with default templates.
# Example Certificate Templates

- User certs - for authentication and encryption.
- Machine certs - for computers to authentication.
- Web enrolment - external cert requests through a web interface.

![[ADCS.webp]]
# Attacks on AD CS

- Exploitable/Misconfigured Template(s)
	- Template creates a direct path for elevation due to insecure settings.
	- Also includes possible abuse to elevate privileges (user/group membership).
	- Insecure changes made to default template (not inherently vulnerable).
- Attack Chains (e.g. NTLMRelay):
	- Default deployment of web enrollment.
	- Most well-known via [[PetitPotam]]
- Exploitable Default Template (i.e. requires patch):
	- Certifried (CVE-2022-26923)
	- Research led to identification of a vulnerable template.
	- Domain computers can enroll in Machine template.
	- Domain users can create domain computers.
	- Any domain user can elevate.