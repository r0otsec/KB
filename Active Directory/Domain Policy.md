---
tags:
  - AD
  - windows
date: 2023-09-1
---
- Refers to [[GPO (Group Policy Object)]] applied at domain level.
- Defines security settings, configurations and rules for all users/computers.
# Default Policy

- Created when domain is made.
- Enforces account policies such as:
	- password length
	- password complexity
	- account lockout settings
	- kerberos settings
- Applies to all domain users and computers.
- Located under `Server Manager` --> `Group Policy Management` --> `Domains`.
# Default DC Policy

- Created by default
- Linked to Domain Controllers [[Organizational Unit (OU)]].
- Defines settings specific to DC security and auditing.
- Located under `Server Manager` --> `Group Policy Management` --> `Domains` --> `Domain Controllers`.
# Usage

- GPOs apply in the following order:
	- `Local` -> `Site` -> `Domain` -> `OU (LSDOU)`