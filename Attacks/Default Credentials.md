---
tags:
  - knowledge
  - attack
date: 2023-09-1
---
- Factory-set usernames/passwords.
- Often come pre-configured on hardware, software, firmware or apps.
- Provided for initial setup but many remain unchanged.
# Why

- Default creds publicly documented in manuals/vendor sites.
- Common in:
	- routers, firewalls, switches
	- ICS/OT (PLCs, HMIs, RTUs)
	- web apps (`Tomcat`, `Jenkins`, `Elasticsearch`, `MongoDB`)
	- internal tools/appliances (printers, NAS, admin panels)
# Offensive Use

- Used during initial access, post-recon or persistence.
- Combined with:
	- [[Shodan]]/Censys searches
	- Subnet scanning for web interfaces, SNMP, Telnet, SSH, etc..
	- ICS/OT environment exploitation.
# Common Tooling

- [[Hydra]]
- [[Ncrack]]
- [[Medusa]]
- [[Patator]]
- Prebuilt lists include:
	- https://github.com/danielmiessler/SecLists
	- https://github.com/ihebski/DefaultCreds-cheat-sheet
	- https://www.rapid7.com/db/search?utf8=%E2%9C%93&search=default+credentials