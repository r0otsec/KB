---
tags:
  - knowledge
  - AD
  - attack
date: 2023-09-1
---
- Attacks that abuse [[ADCS (Active Directory Certificate Services)]] and [[Kerberos]] [[PKINIT authentication|PKINIT]].
- Can be used to:
	- impersonate domain users or computers.
	- escalate privileges to DA or SYSTEM.
	- achieve long-term persistence using legit creds in form of certs.
# PKINIT Recap

- Allows users to authenticate to AD using a cert instead of creds.
- If valid cert gained, you can:
	- authenticate as that user via Kerberos.
	- request a [[Ticket Granting Tickets (TGTs)|TGT]] and impersonate.
	- use tools like [[Certipy]], [[Rubeus]] or [[PKINITtools]].
# ESC1 - ESC14

- 14 certified escalation paths.
- [[ESC1]]:
	- request cert from template
	- allows specifying the SAN
	- lets them impersonate any user (DAs) when authenticating with cert.
- [[ESC2]]:
	- allows unauth subject name specifications.
	- requires no manager approval.
	- if attacker has enrol permissions, can request a cert as any user.
- [[ESC3]]:
	- control over a vulnerable [[Certificate Template|certificate template]] (`WriteProperty`  or `FullControl`).
	- can modify it to allow SAN spoofing or weaken EKUs, then enrol for impersonation.
- [[ESC4]]:
	- control over the CA itself (not template).
	- with `ManageCA` rights, can issue certs using any template or escalate through template abuse.
- [[ESC5]]:
	- abuses Enrolment Agent template.
	- special certs allow users to enrol on behalf of others.
- [[ESC6]]:
	- Enrolment Agent cert (from ESC5).
	- combines with a vulnerable template to issue cert for any user.
- [[ESC7]]:
	- template configured to use `altSecurityIdentities` or UPN mapping.
	- if spoofing identity can be done or cert matches, can login as someone else.
- [[ESC8]]:
	- attacker uses NTLM relay to the AD CS HTTP interface (`certsrv`).
	- if CA accepts web enrollment and template misconfigured:
		- relayed NTLM auth results in cert issued without user knowledge.
- [[ESC9]]:
	- attacker compromises CA's private key.
	- can issue any cert they want, for any identity.
- [[ESC10]]:
	- abuse of misconfigured application policies (EKUs).
		- e.g. template made for machine auth also being used for client auth.
	- allows cross pivoting from machine -> user auth.
- [[ESC11]]:
	- attacker controls AD permissions over cert templates or CA objects.
		- via `WriteDACL` or `GenericAll`.
	- can grant themselves enroll rights or modify templates.
- [[ESC12]]:
	- combines ESC6 with bad delegation.
	- attackers who have enrollment rights and can manipulate target `msDS-KeyCredentialLink`:
		- can create shadow credentials or issue on behalf of certs.
- [[ESC13]]:
	- third-party templates (e.g. [[SCCM (System Center Configuration Manager)|SCCM]], EFS, VPN software) often include dangerous defaults/overly broad access.
	- attackers exploit vendor-supplied configs to escalate.
- [[ESC14]]:
	- insecure public enrollment setup (e.g. AnyCert or anonymous access to `certsrv`).
	- allows attackers to submit arbitrary cert requests without auth:
		- especially dangerous combined with permissive templates.
- [[ESC15]]:
	- attacker controls the security descriptor of the CA object.
	- can modify the CA object permissions to escalate to `ManageCA`.
	- similiar in spirit to ESC4, but achieved via AD permissions.
- [[ESC16]]:
	- attacker controls over user/computer that has dangerous template permissions.
		- user A has enrol rights over vulnerable template.
		- attacker has control over user A.
		- attacker uses path to escalate and request a cert.
# Tooling

- [[Certipy]] - best all-in-one for recon, abuse, auth.
- [[ntlmrelayx]] - used for relaying creds to AD CS HTTP interfaces.
- [[Rubeus]] - supports PKINIT TGT requests using certs.
- [[PKINITtools]] - linux equivalent for requesting TGTs via cert.
# Defenses

- Audit all templates:
	- `ENROLLEE_SUPPLIES_SUBJECT`
	- EKUS: `AnyPurpose`, `ClientAuth`
	- `ManagerApprovalRequired = 0`
- Restrict `Enroll`, `Write` and `ManageCA` rights.
- Disable HTTP enrollment if not required.
- Monitor:
	- cert issuance logs (`Event ID 4886/4887`).
	- PKINIT logons (`Event ID 4768` with cert usage).
- Rotate/revoke any abused certs/templates.

