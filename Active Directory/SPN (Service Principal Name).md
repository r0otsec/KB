---
tags:
  - AD
date: 2023-09-1
---
- Unique identifiers.
- Map service instance to a service account.
- Allows [[Kerberos]] to find which account is responsible for a given service.
- Stored on user, computer or service accounts.
- Managed via the `servicePrincipalName` attribute.
# Format

- `serviceclass/hostname:port`
	- e.g. `MSSQLSvc/db01.corp.local:1433`
# Purpose

- Essential for Kerberos authentication to services
- [[KDC (Key Distribution Center)|KDC]] uses SPNs to:
	- match requested services to correct account.
	- encrypt TGS tickets with target service account's key.
# Enumeration

- To enumerate SPNs with [[PowerShell]]:
	- `Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName`
- To enumerate with [[Impacket Toolkit|Impacket]]:
	- `GetUserSPNs.py <domain>/<user>:<pass>`
# Notes

- SPNs are case-insensitive.
- Common SPN types include:
	- HOST, HTTP, CIFS, MSSQLSvc, LDAP, WSMAN
- Can be used with RC4, AES, or `PKINIT`.


`