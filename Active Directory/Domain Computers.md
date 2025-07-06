---
tags:
  - AD
  - windows
date: 2023-09-1
---
- Any machine joined to the [[Active Directory]] domain.
- Becomes a trusted member and obtains computer account in AD after joining.
- Contains unique SID and account in AD.
- Authenticates using machine account (ending in `$`) and random pass.
- Located under `Server Manager` -> `Users and Computers`.
# Permissions

- Authenticate to the domain using computer account.
- Access shared resources based on permissions.
- Run scheduled tasks, group policies and scripts.