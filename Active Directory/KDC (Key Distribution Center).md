---
tags:
  - AD
  - windows
date: 2023-09-1
---
- Core component of [[Kerberos]] authentication.
- Responsible for issuing tickets allowing users/services to authenticate securely.
- Runs as a service on [[Domain Controller|DC]].
- Two main functions:
	- [[AS (Authentication Server)]] - handles initial login ([[Ticket Granting Tickets (TGTs)|TGT]] issuance)
	- [[Ticket Granting Service (TGS)]] - handles service ticket requests (TGS tickets).
# How It Works

1. User logon - sends request to KDC, receives TGT, encrypted with `krbtgt` key.
2. User requests access to service - sends TGT + service name, receives TGS ticket, encrypted with service's key (from [[SPN (Service Principal Name)|SPN]]).
# Internals

- TGT
	- authenticates user to the domain.
	- encrypted with the `krbgtg` account's password hash.
	- valid for 10 hours by default.
- TGS Ticket
	- used to access specific services (CIFS, HTTP, MYSQL, etc...)
	- encrypted with the target service account's key (based on SPN)
# Attacks

- Attack surface includes:
	- [[Kerberoasting]] - request TGS tickets for SPNs and crack offline
	- [[Pass the Ticket]] - use stolen TGTs to impersonate users.
	- [[Overpass the Hash]] - forge TGT with user's NTLM hash.
	- [[Golden Ticket Attack]] - forge TGT using `krbtgt` hash (persistence).
	- [[Silver Ticket Attack]] - forge TGS ticket using service account hash (targeted access).
# Notes

- Every DC runs a KDC automatically.
- KRBTGT account is a domain-wide key (compromise - full Kerberos abuse).
- KDC logs can reveal suspicious Kerberos activity:
	- Event IDs:
		- `4768`
		- `4769`
		- `4771`
