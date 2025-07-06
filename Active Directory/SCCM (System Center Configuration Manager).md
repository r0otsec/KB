---
tags:
  - knowledge
  - windows
date: 2023-09-1
---
- Enterprise endpoint management platform.
- Used to deploy software, manage patches, push configs, and inventory systems.
- Part of Microsoft Endpoint Manager suite.
# Functions

- Software distributions (install/update/remove apps).
- Patch management (OS and 3rd-party updates).
- OS deployment (image-based provisioning).
- Hardware/software inventory.
- Remote control & compliance enforcement.
- Endpoint protection configuration.
# Architecture

- `SCCM server` - central management point#
- `Site database (SQL Server)` - stores config and deployment data.
- `Distrubition points (DPs)` - hosts deployment files/content.
- `Management points (MPs)` - handle communication with clients.
- `SCCM clients` - installed on managed endpoints (domain-joined systems).
# Attacks

- SCCM clients run actions as SYSTEM.
- Compromising the SCCM server gives central control over domain endpoints.
- SCCM client logs may reveal site info, admin actions, network layouts.
- Check registry:
	- `HKLM\Software\Microsoft\SMS\`
	- `HKLM\Software\Microsoft\CCM\`
- Artifacts:
	- `C:\Windows\CCM\Logs\`
	- `C:\Program Files\Microsoft Configuration Manager\Logs\`
# Notes

- Often installed with high privileges.
- May have stored credentials, embedded scripts, or plain-text config files.
- Commonly targeted due to high trust.

