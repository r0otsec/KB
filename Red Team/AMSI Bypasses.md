---
tags:
  - redteam
  - windows
date: 2023-09-1
---
- [[AMSI (Anti Malware Scanning Interface)|AMSI]]  - Windows API.
- Allows app/services to integrated with installed AV/EDR solutions.
- Scans script-based content at runtime:
	- e.g. [[PowerShell]], `VBSCript` and `JavaScript` before execution.
- Major roadblock in red teams:
	- inspects/often flags post-exploitation tools ([[Cobalt Strike]], [[Empire]]).
# Internals

- Operates as a bridge between scripting engine and underlying antivirus.
- If code is about to execute:
	- it gets handed off to `AmsiScanBuffer`
		- passes content to registered antivirus engine.
		- engine evaluates if the content is malware or contains bad behaviour.
		- if result is `AMSI_RESULT_DETECTED`, script is blocked before execution.
- Part of broader telemetry and enforcement strategy including:
	- `Event Tracing for Windows (ETW)`.
	- Script block logging,
	- Anti tamper mechanisms.
- Especially effective against common [[TTPs (Tactics, Techniques & Procedures)|TTPs]] such as:
	- `IEX` based downloaders
	- encoded payload execution
	- reflective DLL loading
# Relevant API/Signatures

- Core function used to scan buffers of content:

```cpp
HRESULT AmsiScanBuffer(
    HAMSICONTEXT amsiContext,
    PVOID         buffer,
    ULONG         length,
    LPCWSTR       contentName,
    HAMSISESSION  amsiSession,
    AMSI_RESULT   *result
);
```

- Typically resides in `C:\Windows\System32`.
- AV engine must implement interface expected by AMSI to perform sig checks.
- Function commonly hooked by [[EDR (Endpoint Detection and Response)|EDRs]] to monitor for tampering/patch attempts.
# PowerShell Example (Pre-Execution Detection)

```powershell
[System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer
```

- Line commonly used to obtain a delegate for unmanaged function pointers:
	- common precursor to patching AMSI or calling Windows APIs dynamically.
- Use of API is often flagged by EDR heuristics as malicious.
# Detection Techniques

- Detection is split into 3 categories:
	- `Static Analysis`: AV engine/EDR inspects known strings, command structures (e.g. `Invoke-Mimikatz`, `IEX`, base64 blobs).
	- `Behavioural Analysis`: observes runtime patterns like memory tampering, use of suspicious .NET APIs, dynamic method invocation.
	- `Hook-Based Detection`: hooks into functions like `AmsiScanBuffer` and `VirtualProtect` to detect common patching techniques.
# Bypass Techniques

