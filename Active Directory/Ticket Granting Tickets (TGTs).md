- Special type of [[Kerberos]] ticket.
- Issued by the [[AS (Authentication Server)|AS]] of the [[KDC (Key Distribution Center)|KDC]] when a user logs in.
- Proves user identity.
- Used to request service tickets from the [[Ticket Granting Service (TGS)|TGS]].
# How It Works

- User sends an [[AS-REQ (Authentication Request)|AS-REQ]] (username/timestamp) to KDC.
- KDC issues an [[AS-REP (Authentication Service Response)|AS-REP]] containing the TGT.
- The TGT:
	- is encrypted with the KRBTGT account's key.
	- contains user identity, expiration, session key, and authorization data.
- The user uses the TGT to request service tickets via TGS-REQ messages.
# Properties

- Encrypted with KRBTGT account hash.
- Valid for:
	- Default: 10 hours
	- Renewable up to 7 days (configurable).
- Stored in memory (e.g. in [[LSASS (Local Security Authority Subsystem Service)|LSASS]]) and visible via:
	- `klist`
	- `mimikatz sekurlsa::logonpasswords`
	- `Rubeus`
# Detection/Logging

- TGT issuance is logged as `Event ID 4768` on the DC.
- Monitor for:
	- unusual volume of TGTs.
	- TGTs with anomalous lifetimes or forged flags ([[Golden Ticket Attack|Golden Ticket]] indicators)
	- TGTs being reused across multiple hosts ([[Pass The Hash]] behaviour).
# Notes

- TGT does not provide service access - only allows the request of TGS tickets.
- The KRBTGT hash is domain-wide:
	- if compromised = shit hit the fan.
- Deleting or rotating the KRBTGT key invalidates all issued TGTs.

