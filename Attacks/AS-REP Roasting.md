---
tags:
  - knowledge
  - AD
  - windows
  - attack
date: 2023-09-1
---
- Offline [[Kerberos]] attack.
- Targets user accounts not requiring Kerberos pre-authentication.
	- if disabled, can request an encrypted [[AS-REP (Authentication Service Response)|AS-REP]] without knowing user password.
	- AS-REP encrypted with user [[NTLM]] hash (can be brute-forced).
- Two types:
	- `Traditional AS-REP Roasting`
	- `MITM AS-REP Roasting`
# How It Works

1. Traditional AS-REP Roasting:
	- search for pre-auth disabled.
	- request AS-REP without valid creds.
	- receive encrypted response using NTLM hash.
2. MITM AS-REP Roasting:
	- positioned on the network (e.g. [[ARP Spoofing]]).
	- use [[ASRepCatcher]] to intercept/force AS-REPs from clients authenticating to DC.
	- optionally force clients to use RC4 encryption to ease cracking.
# Conditions

- `Classic`: requires accounts with `DONT_REQ_PREAUTH`
- `MITM`: can work against any Kerberos user if you can intercept:
	- ARP spoofing or network-based MITM.
	- use `ASRepCatcher` relay or passive listener mode.
# Tools

- Linux
	- Enumerate vulnerable users:
		- `GetNPUsers.py corp.local/ -no-pass -usersfile users.txt -dc-ip DC_IP`.
	- Crack AS-REP offline:
		- `hashcat -m 18200 -a 0 hashes.txt wordlist.txt`
	- MITM with ASRepCatcher:
		- Relay mode:
			- `ASRepCatcher relay -dc DC_IP`
		- Passive listener:
			- `ASRepCatcher listen`
- Windows:
	- Listing users without pre-auth requirement:
		- `Get-DomainUser -PreauthNotRequired`
	- Requesting AS-REP using [[Rubeus]]:
		- `Rubeus asreproast /domain:corp.local /userlist:users.txt /dc:DC_IP`
# Detection

- Monitor AS-REPs (`Event ID 4768`) for accounts without pre-auth flag.
- Track MITM tools using ARP spoofing or Kerberos coercion.
# Mitigations

- Enable Kerberos pre-auth for all accounts.
- Disable vulnerable accounts/enforce strong passwords.
- Secure internal networks to prevent MITM.
- Detect/block rogue AS-REP intercepts with network monitoring/policy enforcement.