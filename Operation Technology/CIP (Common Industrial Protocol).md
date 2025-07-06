---
tags:
  - Operational-Technology
date: 2023-09-1
---
- Family of protocols including:
	- [[EtherNetIP (ENIP)]]
	- [[DeviceNet]]
	- ControlNet
- Provides common language for devices to share data and commands.
- Most popular with Rockwell/Allen Bradley devices.
- Used to connect:
	- [[PLC (Programmable Logic Controller)|PLCS]]
	- Sensors and [[Actuator|actuators]]
	- [[HMI (Human Machine Interface)|HMIs]]
	- Driver and remote I/O
# Security

- No built-in security in many implementations.
- Vulnerable to various attacks including:
	- Device enumeration
	- Command injection (unprotected EtherNet/IP)
	- Replay/DoS
