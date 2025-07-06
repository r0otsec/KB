---
tags:
  - tool
  - redteam
  - detection
  - knowledge
date: 2023-09-1
---

- Used to invoke very specific TTPs from [[MITRE ATT&CK]] to see if you can detect them in something an EDR like [[Elastic]].

# Executing

- Make sure that you disable AV. This is *NOT* meant to be used to test if your AV will detect it - it is meant to be used to create detections in a SIEM like [[Splunk]] or [[Elastic]].
# Options

- Show actual commands: `Invoke-AtomicTest T1547.001 -ShowDetails`
- Cleanup commands: `Invoke-AtomicTest T1547 -Cleanup`
# Mapping to APT Groups

- CISA creates documents indicating what TTPs they have seen APT groups using. You can take these TTPs and execute them using atomic redteam to create detections for these TTPs.
	- https://www.cisa.gov/news-events/cybersecurity-advisories/aa22-083a
- You can also look at [[Sysmon]] logs that are fired when using atomic redteam. You can use  these to start writing signatures and detections.
- Tip: When you are doing atomic redteam detections, you can set a temp rule to not clutter dashboards with your testing so your SOC is not freaked out.
- [[Adversary Simulation]]
- This helps you do gap analysis.
	- This also helps you create a narrative around your defenses and the offensive techniques.
# References

<div class=iframe-container><iframe width="560" height="315" src="https://www.youtube.com/embed/VTkRkgBjAEA?si=Fv2pYvvIZq3nunNp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

- Installing Atomic Redteam: https://github.com/redcanaryco/invoke-atomicredteam/wiki/Installing-Invoke-AtomicRedTeam