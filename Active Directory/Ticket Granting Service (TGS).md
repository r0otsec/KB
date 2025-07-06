- Component of [[KDC (Key Distribution Center)|KDC]].
- Responsible for issuing service tickets when client wants to access specific service.
- Validates a user's [[Ticket Granting Tickets (TGTs)|TGT]].
- Issues a [[TGS-REP]], including the service ticket.
# How It Works

- User authenticates to the KDC and receives a TGT (via [[AS-REQ (Authentication Request)|AS-REQ]]/[[AS-REP (Authentication Service Response)|AS-REP]]).
- When user wants to access service, sends a TGS-REQ to the TGS.
- The TGS:
	- validates the TGT and client authenticator.
	- creates service ticket.
	- sends it back via TGS-REP.
- User presents ticket to service to gain access.
# Ticket Details

- TGT is encrypted with the KRBTGT account key.
- Service ticket is encrypted with the target service account's key.
- Both tickets include:
	- user identity
	- session keys
	- validity period
	- authorization date (e.g. SIDs, groups)
# Notes

- TGS and [[AS (Authentication Server)|AS]] both run on DCs.
- Kerberos SSO works by allowing TGS to handle repeated service access without re-auth.
- TGS is invoked every time a new SPN is accessed.
# Logging

- `Event ID 4769` logs TGS-REQ/TGS-REP activity on the DC.
- Helpful to track:
	- Which SPNs are being accessed.
	- Unusual or high-volume ticket requests (e.g. [[Kerberoasting]]).


