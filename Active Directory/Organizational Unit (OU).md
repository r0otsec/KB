- Container objects within AD.
- Organizes domain objects (users, computers, groups).
- Applies group policies in a logical way.
# Purpose

- Delegate administrative control.
- Scope [[GPO (Group Policy Object)|GPOs]]
# Properties

- OUs exist within a single domain.
- Can be nested.
- Do not have security principals.
- OUs can contain:
	- users
	- computers
	- groups
	- other OUs
# Management

- Created/managed using:
	- `Active Directory Users and Computers (ADUC)`
- Delegate permissions using:
	- [[ACL (Access Control List)|ACLs]] on OU objects.
- Example use case would be:
	- granting helpdesk group access to reset passwords.
# Attacks

 - Over-permissioned OUs are an abuse opportunity.
 - Users with `WriteProperty`, `GenericAll`, or `WriteDacl` can:
	 - Modify GPO links.
	 - Create users/computers.
	 - Assign [[Resource Based Delegation|RBCD]] permissions.
# Notes

- Different from containers (`CN=`) which are default, non-policy applying AD containers.
- OU-based GPOs apply only to objects directly in the OU.
- Always audit delegation rights to ensure least-privilege access.

