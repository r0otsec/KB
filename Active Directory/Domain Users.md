---
tags:
  - AD
  - windows
date: 2023-09-1
---
- User accounts stored in AD domain.
- Represents individual people, services or apps.
- Authenticates to domain resources and services.
- Located under `Server Manager` -> `Users and Computers`.
# Properties

- Unique [[Security Identifier (SID)|SID]] per user.
- Assigned UPN (e.g. user\@domain.com).
- Password/account policies controlled by Group Policies.
# Default Groups

- New users are added to:
	- Domain Users group.
	- Other groups based on policies/manual assignment.

