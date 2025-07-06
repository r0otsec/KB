---
tags:
  - knowledge
  - methodology
  - windows
  - attack
date: 2023-09-1
---

# Windows Privesc Strategy

1. Check your users and groups
2. Run [[winPEAS]] with fast, searchfast and cmd options.
3. Run [[Seatbelt]] and other scripts
4. If your scripts are failing or you do not want to be noisy, run the commands manually
	- Manual Commands - https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md
5. Avoid rabbit holes by creating a checklist of things you need to do for each privilege escalation method.
6. Read through interesting files in the Desktop or in `C:\` and `C:\Program Files`.
7. If you still don't know where to go, re-read your full enumeration dumps and highlight anything that seems odd.
# Windows Privilege Escalation

- [[Kernel Exploits]]
- [[Service Exploits]]
- [[Registry Exploits]]
- [[Plaintext Passwords]]
- [[Scheduled Tasks]]
- [[Insecure GUI Apps]]
- [[Startup Apps]]
- [[Exploiting Installed Applications]]
- [[Token Impersonation]]
- [[Port Forwarding]]
- [[Get System]]
- [[Potato Exploits]]
# Privesc Tools

[winPEAS](https://github.com/peass-ng/PEASS-ng/releases/tag/20250301-c97fb02a)
[Windows PrivEsc Checklist](https://github.com/evets007/OSCP-Prep-cheatsheet/blob/master/windows-privesc.md)
[Sherlock](https://github.com/rasta-mouse/Sherlock/blob/master/Sherlock.ps1)
[Watson](https://github.com/rasta-mouse/Watson)
[PowerUp](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)
[JAWS](https://github.com/411Hall/JAWS)
[Windows Exploit Suggester](https://github.com/bitsadmin/wesng)
[Metasploit Local Exploit Suggester](https://www.rapid7.com/blog/post/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/)
[Seatbelt](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)
[SharpUp](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries)
# Further Reading

https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/
https://www.fuzzysecurity.com/tutorials/16.html
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md
# Where To Learn

https://institute.sektor7.net/rto-lpe-windows