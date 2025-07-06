---
tags:
  - attack
  - web
date: 2023-09-1
---
- Drupal - widely used CMS.
- Historically vulnerable to critical RCEs.
- Most notably including all `Drupalgeddon` vulnerabilities.
# Recon

- [[Droopescan]] can be used for analysis:
	- `droopescan scan drupal -u http://target --enumerate p,v,m`
	- `p` - plugins/modules
	- `v` - version detection
	- `m` - themes
- Check `/CHANGELOG.txt`:
	- `curl http://target/CHANGELOG.txt | grep Drupal`
- Check `<meta>` version leaks:
	- `curl http://target | grep -i drupal`
- Check admin paths such as:
	- `/user/login`
	- `/user/register`
	- `/node/add`
	- `/admin/modules`
# Drupalgeddon

- [[Drupalgeddon (CVE-2014-3704)]]
- SQL injection -> PHP code injection
- Affected `Drupal 7.x < 7.32`
- Sends crafted POST request to vulnerable endpoint with SQL payload.
- Many available PoCs including [this](https://github.com/Neldeborg/Drupalgeddon-Python3).
# Drupalgeddon2

- [[Drupalgeddon2 (CVE-2018-7600)]]
- RCE via form API render injection.
- Affected `Drupal 7.x < 7.58, 8.3.x < 8.3.9, 8.4.x < 8.4.6, 8.5.x < 8.5.1`
- Unauthenticated users inject malicious render arrays.
- Many available PoCs including [this](https://github.com/lorddemon/drupalgeddon2/tree/master).
# Drupalgeddon3

- [[Drupalgeddon3 (CVE-2018-7602)]]
- Follow up to DG2
- Affected `Drupal 7.x < 7.59`
- Similiar render injection vendor, requires basic user authentication.
- Many available PoCs including [this](https://github.com/oways/SA-CORE-2018-004/tree/master). 
# Tools

- Metasploit modules:
	- `exploit/unix/webapp/drupal_drupalgeddon2`
	- `exploit/unix/webapp/drupal_rest_rce`