---
description: The Adversary Is Trying To Run Malicious Code
---

# ♦️ Execution

Execution, in the realm of cybersecurity, involves implementing strategies that lead to the activation of code controlled by adversaries on a local or remote system. These methods, often paired with other tactics, serve broader objectives like exploring networks or pilfering data. For instance, an adversary may opt to employ a remote access tool for executing a PowerShell script to conduct remote system discovery.

A noteworthy aspect is that many of these techniques do not necessarily rely on specific tools but leverage access and native tools available on the target Windows machine. Opting for execution on Windows-signed binaries strategically helps evade detection by steering clear of creating new processes or network connections, anomalous parent/child relationships, file/registry modifications, memory anomalies, and leaving traces in log files.

Many of these methods don't necessitate specialized tools; rather, they rely on access and leverage the native tools inherent to the Windows machine. Choosing to execute operations on Windows-signed binaries serves a primary purpose of evading detection by:

<mark style="color:orange;">`Avoiding creation of new processes/network connections;`</mark>\
<mark style="color:orange;">`Avoiding creation of anomalous parent/child relationships;`</mark> \
<mark style="color:orange;">`Avoiding creation/modification of files/registry entries;`</mark> \
<mark style="color:orange;">`Avoiding creation of memory anomalies; and,`</mark> \
<mark style="color:orange;">`Avoiding leaving evidence in log files`</mark>
