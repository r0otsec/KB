- [[Kerberos]] message sent by client to the [[Ticket Granting Service (TGS)|TGS]] - part of the [[KDC (Key Distribution Center)|KDC]] - to request access to specific service using a previously issued TGT.
# How It Works

- Occurs after [[AS-REQ (Authentication Request)|AS-REQ]]/[[AS-REP (Authentication Service Response)|AS-REP]] exchange (initial login).
- Client:
	- presents its TGT
	- specifies the SPN it wants to access.
- The KDC's TGS:
	- verifies the TGT.
	- issues a TGS-REP containing the service ticket.
# Structure

The TGS-REQ includes:
- The TGT (proof of identity, encrypted with KRBTGT key)
- The client authenticator (timestamp + session key, encrypted with the TGT’s session key)
- The requested SPN (target service)
# Notes

- Occurs every time a user/service wants to access a Kerberos-protected resource.
- Logged on the DC as `Event ID 4769`.
- Required for each unique SPN a user accesses.
- [[Kerberos Delegation]] relies on chained TGS-REQ/TGS-REP operations.


