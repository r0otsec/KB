---
tags:
  - knowledge
  - AD
  - windows
date: 2023-09-1
---
- Network authentication protocol used by Active Directory.
- Relies on tickets and symmetric cryptography to verify identifies securely.
- Reduces credential exposure compared to older protocols (e.g. [[NTLM]]).
- Default auth protocol in Windows domains since Windows 2000.
# Core Components

| Component                         | Description                                       |
| --------------------------------- | ------------------------------------------------- |
| Client                            | User or service requesting access.                |
| [[KDC (Key Distribution Center)]] | Issues tickets; runs on DCs, contains, AS and TGS |
| [[AS (Authentication Server)]]    | Issues [[Ticket Granting Tickets (TGTs)]]         |
| [[Ticket Granting Service (TGS)]] | Issues service tickets                            |
| KRBTGT                            | Hidden domain account used to encrypt/sign TGTs   |
| [[SPN (Service Principal Name)]]  | Unique identifier for service account.            |
# Authentication Flow

1. [[AS-REQ (Authentication Request)|AS-REQ]] (user -> KDC):
	- client requests TGT using username + timestamp (encrypted with user's password-derived key).
2. [[AS-REP (Authentication Service Response)|AS-REP]] (KDC -> user):
	- KDC returns TGT (encrypted with `krbtgt`) and session key.
3. [[TGS-REQ]] (user -> KDC):
	- client presents TGT and asks for access to a specific service (SPN).
4. [[TGS-REP]] (KDC -> user):
	- KDC returns a TGS ticket encrypted with the service account's key.
5. Client -> Service:
	- sends TGS to the target service to authenticate.

![[Kerberos Flow.png]]
# Notes

- TGT lifetime - 10 hours by default (renewable up to 7 days).
- Relies heavily on accurate system time (clock skew > 5 minutes = failure).
- All DCs act as KDCs.
# Detection

- Monitor the following Event IDs:
	- `4768` - TGT issued.
	- `4769` - TGS issued.
	- `4771` - failed pre-auth.
- Unusual volume of TGS requests (roasting).
- TGTs issued for long durations or forged ticket indicators.


