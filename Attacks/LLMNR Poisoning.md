---
tags:
  - attack
  - knowledge
  - AD
  - windows
date: 2023-09-1
---

- LLMNR Poisoning can be used for two different things:
	- [[SMB Relay]]
	- Cracking Hashes
- Uses [[Responder]] to send message back to requesting host
- `responder -I eth0 -rdwv`
- Once traffic has been poisoned, hashes can be cracked using [[Hashcat]] or relayed using [[SMB Relay]].
# Defense

- Disable [[LLMNR]] and NBT-NS in GPOs.
- Instead of cracking the hashes from LLMNR, you can relay the hashes.
	- [[SMB]] signing must be disabled on the target.