---
tags:
  - AD
  - windows
date: 2023-09-1
---
- Used to manage access control in AD by grouping users, computers, objects together.
- Simplifies admin of permissions and rights for multiple objects.
- List group name, scope and description via:
	- `Get-ADGroup -Filter * | Select-Object Name, GroupScope, Description`.
# Types

- `Global Groups`:
	- contain users/groups from same domain
	- can be granted permissions in other domains.
- `Domain Local Groups`:
	- grant permissions within same domain.
	- can contain members from any domain.
- `Universal Groups`:
	- used across domains/forests
	- contain members from any domain in the [[Forest|forest]].
# Group Scopes

- `Global Group Scope`:
	- used to group users with similiar needs in same domain.
	- can eb nested into domain local groups.
- `Domain Local Group Scope`:
	- assign permissions to resources within domain.
	- can contain any type of objects (users from other domains too).
- `Universal Group Scope`:
	- suited for larger environments with multiple domains.
	- can include members from any domain in the forest.