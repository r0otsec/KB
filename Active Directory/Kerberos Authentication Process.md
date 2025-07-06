The entire process for Kerberos can be found below:

1. User Logs in -> `AS-REQ`:
	- User enters their username and password (or smart card if using [[PKINIT authentication|PKINIT]]).
	- Client generates an Authenticator (timestamp) and sends it to the [[AS (Authentication Server)|AS]] on the [[Domain Controller|DC]].
	- This is the `AS-REQ`.
2. DC sends back a TGT -> `AS-REP`:
	- DC verifies the user's password.
	- If correct, it returns a [[Ticket Granting Tickets (TGTs)|TGT]] in the [[AS-REP (Authentication Service Response)|AS-REP]].
		- TGT is encrypted using the [[KRBTGT]] account's secret key.
		- Only the [[KDC (Key Distribution Center)|KDC]] can decrypt it (like a signed user identity).
	- At this point, user is authenticated but still needs permission to access services.
3. User wants to access a service (e.g. file share) -> `TGS-REQ`:
	- Client sends a [[TGS-REQ]] to the [[Ticket Granting Service (TGS)|TGS]] (also on DC).
		- It includes the TGT and request for a specific service, identified by an [[SPN (Service Principal Name)|SPN]].
4. DC sends a service ticket -> `TGS-REP`:
	- TGS verifies the TGT and client.
	- It sends back a TGS (service ticket) inside a [[TGS-REP]].
		- Service ticket is encrypted with the service account's key.
		- Only target service can read it.
	- User now has proof they are allowed to access a specific service.
5. User contacts the service -> `Authenticated Access`:
	- Client sends the service ticket to the target server (e.g. file server).
	- Service decrypts the ticket using its own key.
	- If valid, grants access as the user specified in the ticket.
# Summary of Messages

| Message | Purpose                      |
| ------- | ---------------------------- |
| AS-REQ  | "Hey DC, I'm logging in"     |
| AS-REP  | "Here's your TGT"            |
| TGS-REQ | "I need access to a service" |
| TGS-REP | "Here's your service ticket" |

