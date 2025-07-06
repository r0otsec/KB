---
tags:
  - knowledge
  - AD
date: 2023-09-1
---

- Directory service by Microsoft to manage identities, authentication, and access control in an enterprise Windows environment.
- Maintains database of objects like users, computers, groups and policies.
- Centralized authentication via [[Kerberos]] and authorization through [[ACL (Access Control List)|ACLs]].
# Core Concepts

- Domain
	- logical grouping of objects.
	- sharing common directory database and policies
	- has a unique ID (Domain SID).
- Domain SID
	- unique ID
	- all principals have SIDs beginning with domain SID
	- `S-1-5-21-<domain-id>-<RID>`
- RID
	- suffix appended to domain SID for each unique object.
	- RID 500 reserved for default domain Administrator
- Domain Controller
	- server hosting AD database
	- responsible for AAA, replication and [[GPO (Group Policy Object)|GPO]] enforcement.
- Organizational Unit (OU)
	- container object to group objects for delegation and policies.
- Forest
	- contains one or more domains.
	- share the same schema, config and global catalog.
- Tree
	- set of domains with a contiguous namespace within a forest.
- Global Catalog
	- partial replica of all objects used to speed up searches/logins
	- hosted on selected DCs.
# Trusts

- Relationships between domains/forests allowing cross-authentication.

>[!danger] Attacks
>See [[Attacks Index]] for common techniques targeting AD environments.