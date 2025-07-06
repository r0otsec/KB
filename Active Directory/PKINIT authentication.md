- Extension to [[Kerberos]].
- Allows users to authenticate using asymmetric cryptography (certs).
- Enables smart card logon or cert based logons.
- Required for Windows Hello for Business, smart card, and shadow cred scenarios.
# How It Works

- During [[AS-REQ (Authentication Request)|AS-REQ]]:
	- client presents a user cert.
	- private key signs part of the request.
	- [[KDC (Key Distribution Center)|KDC]] verifies signature using public key from cert.
	- if valid, KDC issues the [[Ticket Granting Tickets (TGTs)|TGT]].
- Uses X.509 certs from:
	- a trusted enterprise [[Certificate Authority (CA)|CA]] (typically [[ADCS (Active Directory Certificate Services)|AD CS]]).
	- smart card token.
# Requirements

- User accounts must have:
	- a certificate mapped to it (UPN/SID mapping).
	- or a valid `msDS-KeyCredentialLink` (for WHfB or shadow creds).
- Domain must:
	- support PKINIT (modern KDC + cert infrastructure).
	- trust the issuing CA.
# Detection/Defense

- For monitoring purposes:
	- Kerberos Event ID `4768`:
		- look for `Certificate Information` in AS-REQs.
	- sudden cert-based logons from systems that don't use them.
- For hardening:
	- lock down `msDS-KeyCredentialLink` write access.
	- secure the NTAuth store.
	- Use cert revocation + short cert lifetimes.

