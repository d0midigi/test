# What %WINDIR%\win.ini / System.ini in Enumeration Means

In the world of Windows forensics and local enumeration, stumbling upon `win.ini` or `system.ini` is like finding a vintage roadmap in a modern GPS world. While they aren't as powerful as they were in the 16-bit era, they still hold significant value for an attacker or a system auditor.

Here is the breakdown of what these files signify during an enumeration process:

### 1. Legacy Configuration & Compatibility

Both files date back to Windows 3.x. Back then, Windows didn't have a centralized Registry. Instead, it relied on these `.ini` files to tell the OS how to behave and how to load drivers.

* `win.ini`: Traditionally handled user-specific settings like fonts, wallpaper, and languages.
* `system.ini`: Handled hardware-specific settings, drivers, and the "shell."

### 2. Persistence Mechanisms (The "Red Flag")

From a security perspective, these files are interesting because they can still be used to execute programs automatically.

* The `run=` and `load=` lines: In `win.ini`, these lines can be modified to execute a malicious binary every time a user logs in.
* The `shell=` line: In `system.ini`, the default is `shell=explorer.exe`. If an attacker changes this to `shell=explorer.exe, malware.exe`, their code will run upon boot.

### 3. Information Gathering

If you are performing enumeration, these files provide a snapshot of the system's environment:

* Active Drivers: `system.ini` lists the drivers being loaded by the kernel.
* Custom Applications: Some legacy (but critical) enterprise software still writes configuration data to these files rather than the Registry.

### 4. Why Check Them Today?

You might wonder why we care about files from 1992.

1. Registry Evasion: Many modern EDR (Endpoint Detection and Response) tools monitor common Registry "Run" keys closely. They might not be as strictly monitoring a legacy `.ini` file for execution.
2. LFI (Local File Inclusion): In web penetration testing, if you find a Local File Inclusion vulnerability on a Windows-based web server, `C:\Windows\win.ini` is a "go-to" file to prove you have file read access because it is almost always present and readable by low-privileged users.

#### Comparison at a Glance

| **File**     | **Primary Focus**             | **Security Interest**                   |
| ------------ | ----------------------------- | --------------------------------------- |
| `win.ini`    | User environment & appearance | Auto-loading apps via `run=` or `load=` |
| `system.ini` | System hardware & drivers     | Modifying the boot `shell`              |

