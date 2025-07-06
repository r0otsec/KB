---
tags:
  - knowledge
  - AD
  - windows
  - redteam
  - attack
date: 2023-09-1
---

- Kerberoasting is a [[Post Exploitation]] attack on service accounts in [[Active Directory]]. The user impersonates an account user with a service principle name (SPN) and requests a service-related ticket. They then crack the password hash linked to that service account and login with plaintext creds.
- Once an attacker successfully cracks the password hash, they can gain unauthorized access to the targeted service accounts and potentially move laterally through the network.

>Cracks service accounts (?) These are often set up as domain admin accounts.

- Kerberoasting can be done with [[Rubeus]]
# Attack Chain

>Note that the domain.local/username:password is of a domain user, not a service account.

1. Use [[GetUserSPNs.py]]: `GetUserSPNs.py domain.local/username:password -dc-ip 192.168.1.123 -request`
2. Copy KRB5tgs hash
3. Crack hash with [[Hashcat]]: `hashcat -m 13100 hashes.txt rockyou.txt -O`
# Defenses

- You are abusing a *feature* of windows
	- Have **VERY** strong passwords
	- Do not make your domain accounts domain administrators