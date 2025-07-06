---
tags:
  - windows
date: 2023-09-1
---
 - Dynamic Link Library
 - Compiled code module.
 - Provides shared functions (GUI elements, file ops, crypto, networking).
# Purpose/Behaviour

- Contain reusable functions and resources
	- e.g. `user32.dll` (UI), `kernel32.dll` (core Windows), `advapi32.dll` (registry, services). 
- Apps dynamically load them at runtime.
# How DLLS are Loaded

- Can be loaded via:
	- `Static linking` (declared at compile time).
	- `Dynamic loading` (e.g. `LoadLibrary`, `GetProcAddress`).
- Windows searches for DLLS in a default order:
	- `Application directory`.
	- `System32`.
	- `Windows directory`.
	- `Current working directory`.
	- `%PATH% directories`.
# Security

- Prime target for threat actors:
	- [[DLL Hijacking]] - drops malicious DLL where program loads it first.
	- `DLL Search Order Abuse` - take advantage of insecure loading paths.
	- [[DLL Injection]] - force process to load DLL (e.g. via `CreateRemoteThread`).
	- [[Reflective DLL Injection]] - load DLL from memory.
- Some common tools include:
	- `SetDLLDirectory`, `LoadLibrary`, `RUNDLL32` and `dllhost.exe`.
	- [[Cobalt Strike]], [[Meterpreter]], [[syringe]], [[Invoke-ReflectivePEInjection]].
# Defenses

- Monitor for
	- unusual DLL loads (`Sysmon Event ID 7`).
	- DLLS loaded from non-standard directories.
	- unsigned/unexpected DLLs in critical processes.
- Some useful commands include:
	- `Get-Process | ForEachObject { $_.Modules }`
	- `tasklist /m`
# Notes

- DLLs uses `.dll` extension but also use `.oxc`, `.drv` and `.cpl`.
- Loaded into virtual address space of calling process.
- Legit DLLs are digitally signed by Microsoft.
