---
tags:
  - knowledge
  - attack
date: 2023-09-1
---
- Automated attack using previously leaked/stolen creds against accounts.
- Leverages password reuse.
- Uses `real` credentials harvested from breaches/leaks.
# Use Cases

- Targets:
	- Web portals (VPN, OWA, Citrix, RDWeb, webmail, SSO).
	- Cloud services (Azure AD, M365, Okta).
	- Internal apps.
# Tools

- [[Kerbrute]] can be used:
	- `kerbrute passwordspray -d corp.local --dc 192.168.1.1 userpass.txt`
- [[Ncrack]] can also be used:
	- `ncrack -p 22 -U users.txt -P creds.txt ssh://target`
- [[H8mail]]:
	- `h8mail -t users.txt -p rockyou.txt -c breaches.csv`
- [[O365creeper]]:
	- `python3 o365creeper.py -e emails.txt -p passwords.txt`
# Credential Sources

- Have I Been Pwned.
- Leaked combo lists from forums/darknets.
- Previously dumped creds from internal ops (`secretsdump`, `mimikatz`, `ntds.dit`, etc..).
# Detections

- Large volumes of login attempts with many unique username/password combos.
- Multiple failed attempts from one IP against many accounts.
- Successful logins from unexpected geos.
- Monitor:
	- web server logs (HTTP 401/403)
	- VPN/firewall auth logs.
	- Azure AD sign-in logs, Okta auth events.
# Mitigation

- Enforce MFA on external-facing apps.
- Monitor for stuffing patterns.
- Use rate-limiting, CAPTCHA, and account lockout.
- Monitor for creds in public breaches.

