- Unique identifier.
- Assigned to users, groups, computers & other security principals.
- Used internally by Windows/AD to enforce permissions, ownership and auditing.
# Format

- SIDs are persistent/unique - they do not change, even if the name does.
- Typical format:
	- `S-1-5-21-<DomainID>-<RelativeID>`
		- `S-1-5-21` - base identifier for domain objects.
		- `<DomainID>` - unique to each domain.
		- `<Relative ID (RID)>` - unique per object (e.g. 500 = Administrator).
# Common RIDS

| RID   | Description            |
| ----- | ---------------------- |
| 500   | Built-in Administrator |
| 501   | Guest                  |
| 512   | Domain Admins group    |
| 513   | Domain Users group     |
| 519   | Enterprise Admins      |
| 1000+ | Custom users/groups    |
# Attacks

- SIDs appear in:
	- [[ACE (Access Control Entries)|ACEs]]
	- Token impersonation attacks
	- Kerberos tickets
- Attack use cases include:
	- [[SID History Injection]]:
		- add a privileged SID to another account's SIDHistory attribute.
		- Grants effective access without group membership.
	- Well-known SIDs can be targeted.
# Notes

- SIDs are globally unique within a domain.
- SIDHistory is often abused in post-exploitation.
- Enumerate with SIDs:
	- `Get-ADUser user1 -Properties objectSID`
