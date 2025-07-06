---
tags:
  - knowledge
  - AD
  - windows
date: 2023-09-1
---
- Trust relationship between two separate AD forests.
- Allows cross-forest authentication and resource access.
- Enables users in one forest to access resources in another.
- Typically used during mergers, acquisitions, or multi-org collaboration.
# Trust Types

- One-way trust:
	- users from Forest A can access resources in Forest B but not vice-versa.
- Two-way trust:
	- users in both forests can access each other's resources.
# Trust Security

- Transitive:
	- forest trusts are transitive (can extend through other trusts within each forest).
- Authentication Types:
	- Selective authentication:
		- access must be explicitly allowed.
	- Forest-wide authentication:
		- all users in trusted forest are treated as authenticated.

