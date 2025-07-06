---
tags:
  - knowledge
  - linux
  - windows
  - networking
date: 2023-09-1
---

- SOCKS proxy (short for socket secure) exchanges network packets between a client and server. We can use these offensively by turning the C2 server into a SOCKS proxy to tunnel external tooling into an internal network.
- This can be helpful when running python tools on Windows machine. This also helps with OPSEC since we are not pushing offensive tooling onto the target or even executing code on a compromised endpoint.
- SOCKS5 supports authentication and has some additional logging capabilities.
- Config file is at `/etc/proxychains.conf`.
# SOCKS5

- To authenticate to socks5 proxy, add `socks5 127.0.0.1 <port> <socks_username> <socks_password>` to `/etc/proxychains.conf`.