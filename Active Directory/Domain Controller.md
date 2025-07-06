---
tags:
  - AD
date: 2023-09-1
---
- Core server in AD that manages and stores the domain database.
- Handles authentication, authorization and directory lookups for [[domain users]] and [[domain computers]].
- Hosts services such as the [[KDC (Key Distribution Center)|KDC]], [[LDAP (Lightweight Directory Access Protocol)|LDAP]] and Group Policy engine.
- List of DCs under `Server Manager` -> `AD DS`.
# Behaviour

- Authenticates logins using [[Kerberos]] or [[NTLM]].
- Distributes [[GPO (Group Policy Object)|GPOs]] to domain machines.
- Responds to directory queries and updates via LDAP.
- Replicates AD data to other DCs for consistency.
# Security

- Compromising DC provides full control over the domain.
- Holds password hashes of all users inside [[NTDS.dit]] file.
- Targeted by tools like [[Mimikatz]] or attacks such as [[DCSync Attack|DCSync]] and [[Golden Ticket Attack|Golden Ticket]].

