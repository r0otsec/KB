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
- Allows attacker to request a cert for any user/service account.
	- achieved by specifying a custom `Subject Alternative Name (SAN)`.
- If template:
	- allows requester to supply the subject.
	- AND supports client authentication ([[PKINIT authentication|PKINIT]])
		- attacker can impersonate any principal in AD.
# Certificate Template Background

- A [[Certificate Template]] is a blueprint, defining:
	- what type of certs can be issued
	- what crypto properties they have
	- what `EKUs` are present
	- who is allowed to request them (via the `Enroll` right)
	- what subject info (like UPN/DNS name) gets inserted into the cert.
- Templates populate the subject from:
	- [[Active Directory]] (controlled/secure).
	- OR let the requester specify the subject (bad!).
- If flag `ENROLLEE_SUPPLIES_SUBJECT` is set, user can tell the [[Certificate Authority (CA)|CA]]:
	- "I want this cert to say it is for `Administrator@corp.local`"
- If template also includes `EKU Client Authentication`, resulting cert can be used for [[Kerberos]] PKINIT login as the spoofed user.
# SAN Background

- SAN field used to associate identities (e.g. UPNs, DNS names) with the cert.
- If SAN includes a UPN like `Administrator@corp.local`, AD accepts it as belonging to that user if the cert chains to a trusted CA.
- AD does not verify the requester of the cert is the user listed in the SAN.
# PKINIT Background

- Extension to Kerberos.
- Allows user to authenticate using a cert instead of password.
- How it works:
	- User sends cert in the [[AS-REQ (Authentication Request)|AS-REQ]] to the [[KDC (Key Distribution Center)|KDC]].
	- KDC checks:
		- is this a trusted CA?
		- does the cert have client authentication EKU?
		- does the UPN in the SAN match a real user?
	- If yes, [[Ticket Granting Tickets (TGTs)|TGT]] is issued.
- If attacker gets a cert that:
	- chains to a trusted CA
	- has the ClientAuth EKU
	- Contains the SAN: `Administrator@corp.local`
- They can authenticate as Administrator.
# Trust Model Failure

- CA will:
	- issue certs with whatever SAN you ask for (if `ENROLLEE_SUPPLIES_SUBJECT`).
	- as long as you are authorized to request something from the template.
- AD will:
	- accept any cert with a trusted chain + valid SAN.
	- regardless of who requested it.

>[!danger]
>Any domain user with enroll rights on a vulnerable template can impersonate any user in AD.
# Exploitation

- Find a vulnerable template via [[Certipy]]:
	- `certipy-ad find -u user@corp.local -p 'Pass123!' -dc-ip 10.0.0.5 -vulnerable`
	- Look for:
		- `ENROLLEE_SUPPLIES_SUBJECT: True`
		- `EKU: Client Authentication`
		- User has `Enroll` rights.
- Request cert impersonating Administrator:
	- `certipy-ad req -u user@corp.local -p 'Pass123!' -ca corp-CA -template CorpTemplate -upn Administrator@corp.local -dc-ip 10.0.0.5 -output esc1`
- Authenticate with forged ticket:
	- `certipy-ad auth -pfx esc1.pfx -dc-ip 10.0.0.5`
	- `gettgtpkinit.py -pfx esc1.pfx corp.local/Administrator`
# Detection & Logging

- `Event ID 4886` (certificate issued).
- Check for mismatch between certificate SAN and requester.
- `Event ID 4768` (Kerberos AS-REQ):
	- logons with certs where the subject != request.
- Certs issued via template with `ENROLLEE_SUPPLIES_SUBJECT = 1`.
# Mitigation

- Audit templates:
	- `certutil -template`
- Disable SAN spoofing:
	- Uncheck `Supply in the request`.
	- Set subject to `Build from this Active Directory information`.
- Restrict enroll permissions.
- Use Manager Approval for sensitive templates.
- Monitor for:
	- certs with suspicious SANs.
	- cert-based logins as high-priv accounts.
