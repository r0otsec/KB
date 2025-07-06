---
tags:
  - technologies
  - web
date: 2023-09-1
---
- Open-source Java web server and servlet container.
- Primarily used to host Java web apps (WAR files).
- Supports:
	- [[Java Servlets]]
	- [[JavaServer Pages (JSP)]]
	- [[WebSocket]]
	- [[Expression Language (EL)]]
- Serves as backend for enterprise apps.
# Key Components

- `Catalina`: core servlet engine (handles HTTP requests/responses).
- `Coyote`: HTTP connector that listens for requests (on port 8080).
- `Jasper`: JSP engine (compiles JSP to Java bytecode).
- `Manager App`: web interface for managing WAR deployments (admin panel).
# Tomcat Structure

- Typical file paths on Linux include:
	- `/usr/share/tomcat`
	- `/var/lib/tomcat/webapps/` - deployed apps
	- `/etc/tomcat` - config files
	- `/var/log/tomcat` - logs