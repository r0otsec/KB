---
tags:
  - AD
  - windows
date: 2023-09-1
---
- [[Kerberos]] feature allowing a service to impersonate a user.
- Common in web apps, SQL servers, front-end/back-end service chains.
- Example:
	- web server receives a user request and needs to query a file share or database as that user.
# Types of Delegation

- [[Unconstrained Delegation]]
	- service receives user's TGT and can impersonate them to any other service.
	- set via `Trust this computer for delegation to any service (Kerberos only)`.
- [[Constrained Delegation]]
	- limits which services the delegated account can access.
	- set via `Trust this user/computer for delegation to specified services only`.
	- uses [[SPN (Service Principal Name)|SPNs]] to define allowed targets.
- [[Resource Based Delegation]]
	- configured on target service account.
	- lets target service decide which accounts are allowed to impersonate users to it.