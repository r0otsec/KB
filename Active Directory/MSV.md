---
tags:
  - AD
  - windows
  - knowledge
date: 2023-09-1
---
- MSV1_0 is the [[NTLM]] authentication provider in Windows.
- Responsible for local/domain authentication when [[Kerberos]] is not used.
# Function

- Used for:
	- local logons
	- NTLM-based network authentication
	- fallback when Kerberos is not available.
- Implements [[NTLMv1]]/[[NTLMv2]] protocols.
- Works with:
	- Winlogon
	- [[LSASS (Local Security Authority Subsystem Service)]]
	- Credential providers.
# Notes

- Still widely supported for backwards compatibility.
- NTLM enabled by default in most environments.
- NTLM fallback occurs when:
	- SPNs are misconfigured.
	- Kerberos pre-auth fails.
	- Hostname used instead of FQDN.

