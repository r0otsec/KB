---
tags:
  - knowledge
  - AD
date: 2023-09-1
---
- Relationships between two domains.
- Allow users in one domain to access resources in another.
- Can be `one-way` or `two-way`.
- Stored/managed by Kerberos trust and NTLM authentication models.
- Located under `Server Manager` -> `Domains and Trusts`
# Types

- Parent/Child:
	- automatic when domains created under same forest.
	- two-way transitive.
- Tree-Root:
	- automatic between tree roots in same forest.
	- two-way transitive.
- External:
	- manual trust with AD domain outside forest.
	- one-way or two-way transitive.
- Forest:
	- manual trust between two forests.
	- one-way or two-way transitive.
- Realm:
	- between AD domain and non-Windows Kerberos realm.
	- one-way or two-way.
# One Way vs Two Way

- One-way trust:
	- Domain A trusts Domain B:
		- Users in domain B can access resources in domain A.
		- Users in domain A cannot access domain B unless separate trust exists.
- Two-way trust:
	- Domain A trusts Domain B, and vice versa:
		- Users in both can access resources in the other.
# Transitive vs Non-Transitive

- Transitive trust:
	- extends beyond two domains involved.
	- domain A trusts domain B, domain B trusts domain C
	- if transitive, domain A also trusts domain C.
- Non-transitive trust:
	- trust not extended between two domains.
	- if domain B trusts domain C, domain A does not.
