---
tags:
  - knowledge
  - AD
date: 2023-09-1
---
- Allows service to impersonate a user and access resources as them.
- Safer than [[Unconstrained Delegation]] as limited and controlled.
- Common where a web server needs to access other services as the user.
# How It Works

- Account set to "trusted for delegation" for named services.
- Services listed in the `msDS-AllowedToDelegateTo` field.
# Example

- User authenticates to constrained delegated account
- Account is limited to delegating authentication to SQL service only

![[CD.webp]]
# Implementation

- Kerberos implements this via two extensions:
	- `Service for User to Self (S4U2Self)`: allows a service to request ticket on behalf of a user.
	- `Service for User to Proxy (S4U2Proxy)`: allows a service to impersonate a user and access other services.
