```dataview
table tag as "Tag", length(rows) as "Frequency"
from ""
flatten file.tags as tag
group by tag
sort length(rows) desc
```

| Tag          | Description                                                                         |
| ------------ | ----------------------------------------------------------------------------------- |
| AD           | Covers AD concepts, services, and infrastructure used in enterprise environments.   |
| Attacks      | Offensive techniques, tactics and procedures used to compromise, escalate, persist. |
| Blue Team    | Defensive strategies, tools, detection methods, and response practices.             |
| CVE          | Vulnerabilities with assigned CVE identifiers.                                      |
| Detection    | Methods and tooling to identify malicious or suspicious activity.                   |
| Evasion      | Techniques used to avoid detection by AV, EDR or defenders.                         |
| Knowledge    | Conceptual notes and foundational understanding.                                    |
| Linux        | Covers Linux systems, commands, and security mechanisms.                            |
| Malware      | Malware development, analysis and behaviour.                                        |
| Methodology  | Structured approaches to hacking, testing or responding.                            |
| Networking   | Covers concepts related to network protocols, infrastructure and enumeration.       |
| OSINT        | OSINT related activities, tools and platforms.                                      |
| Phishing     | Email-based and social engineering attack techniques, defenses and tactics/tools.   |
| Pivoting     | Techniques/strategies used to move within a network or to other networks.           |
| Port-Scan    | Discovery techniques and tools focused on identifying open ports and services.      |
| Post-Ex      | Tools and techniques used after exploitation.                                       |
| PowerShell   | PowerShell-specific notes for offensive and defensive uses.                         |
| Programming  | Language specific notes and security concepts for languages.                        |
| Protocols    | Communication protocols at all layers.                                              |
| Red Team     | Simulated attacker tactics and more advanced techniques.                            |
| Technologies | General IT systems or platforms.                                                    |
| Tool         | Standalone utilities or tools used in testing, red teaming or defense.              |
| Web          | Web application security and protocols.                                             |
| Windows      | Notes specific to the Windows OS.                                                   |

```dataview
table file.name as "Note Name"
```