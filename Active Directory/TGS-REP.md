- [[Kerberos]] response message sent by [[KDC (Key Distribution Center)|KDC]] [[Ticket Granting Service (TGS)|TGS]] after client requests access to service via [[TGS-REQ]].
- Contains service ticket client uses to authenticate to that service.
# How It Works

- Triggered after a user presents a TGT to the KDC and requests access to a specific [[SPN (Service Principal Name)|SPN]].
- KDC:
	- validates the TGT and user's authorization.
	- issues a TGS-REP which includes:
		- service ticket (encrypted with the service account key)
		- session key for communication with the service
- Client never sends password.
# Attacks

- TGS-REP is key message involved in [[Kerberoasting]]:
	- any domain user can send a TGS-REQ for service account with registered SPN.
	- returned TGS-REP contains encrypted service ticket.
	- ticket cracked offline to recover service account's NTLM hash.
# Detection/Defense

- TGS-REP events have `Event ID 4769`.
- Monitor for:
	- multiple TGS requests in a short period.
	- request for high-privilege SPNs.
	- anomalous users requesting TGS for services they don't access.
# Notes

- TGS-REP is part of the normal Kerberos flow:
	- `AS-REQ` -> `AS-REP` -> `TGS-REQ` -> `TGS-REP`
- Service ticket encrypted with the target service's key - why it is crackable during Kerberoasting.