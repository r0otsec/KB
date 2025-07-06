- Built-in, hidden account in every AD domain.
- Acts as the secret key holder for [[Kerberos]].
- Used to sign and encrypt all [[Ticket Granting Tickets (TGTs)|TGTs]] (Ticket Granting Tickets) issued by the domain.
# Characteristics

- Not used for logon - cannot be used as a normal account.
- Password never expires but can be changed periodically.
- Every TGT is encrypted with the KRBTGT account's NTLM or AES key.
- Exists in every domain, and is domain-specific.
# Attacks

- If attacker obtains hash, they can:
	- Forge TGTs for any user.
	- Create [[Golden Ticket Attack|Golden Tickets]].
- Common methods to dump KRBTGT hash include:
	- `mimikatz lsadump::dcsync /user:krbtgt`
	- `secretsdump.py`
# Defender Notes

- Rotate the KRBTGT password regularly.
- Monitor for:
	- unauthorized access to the KRBTGT account.
	- Abnormal TGT lifetimes or PAC anomalies.
- Event IDs to monitor:
	- `4768` - TGT issued.
	- `4769` - TGT issued with forged or impossible SIDs.