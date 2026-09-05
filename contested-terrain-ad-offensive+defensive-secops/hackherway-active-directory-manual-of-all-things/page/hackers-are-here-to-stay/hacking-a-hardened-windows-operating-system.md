# Hacking a Hardened Windows Operating System

Hacking a Hardened Windows Operating System

In this section, we will discuss security hardening implementations for operating systems, specifically Microsoft Windows operating systems with secure configurations that are enforced by Active Directory Group Policy Object (AD GPO) settings and to showcase ways to bypass these hardened measures. It is important to remember that hardening configurations can be a whole series of various and different settings depending on the benchmark or hardening guide used as well as the OS that is in preparation for hardening. For this section, however, we will examine some specific settings, and in real hardened environments have a 50/50 chance of working if you know your stuff; however, the overall methodology still applies.

General Methods for Breaking Group Policy Object (GPO) Hardening Policy Implementations

Scenario 1 – Local Admin on a Machine with Some Hardening in Place:

For starters, there is one thing to know about Group Policy Object enforcement and that is that all Group Policy configurations, settings, and policies, no matter what changes made to an asset, a group of assets, or the domain as a whole enforces on 90 minute cycle meaning essentially that every 90 minutes all reporting and live hosts on a network connected to the AD receive policy enforcement updates every 90 minutes. This timing interval can be configured in AD GPO, but 90 minutes has always been the norm for policy enforcement. Also, if you need to deploy a change in policy and need to have it immediately applied to whatever entity it is you’re focused on, you can force GPO policy enforcement by typing this command in the command line or PowerShell terminal:

gpupdate /force

This explains how you, as an admin, a hacker, an engineer, an analyst, a manager, can change Group Policy settings and basically get away with it. Of course, if auditing is enabled, then the Windows Event Viewer will log all activities imparted onto domain controllers, servers, and workstations. If you have local admin privileges on any machine, it’s pretty simple to break hardening measures, so it doesn’t necessarily mean that you need Domain or Global Admin privileges to accomplish this.

Scenario 2 – Normal User on a Machine with Some Hardening Measures in Place:

Let’s say you have access to a machine and realize that the users have some hardening in place. The question is, how can you bypass or stop the hardening? Thanks to David Wells at Tenable, we can use this as a general technique: https://medium.com/tenable-techblog/bypass-windows-10-user-group-policy-and-more-with-this-one-weird-trick-552d4bc5cc1b

TL;DR: Grab a copy of the ntuser.dat file under C:\Users\\%username%folder (or create a new one on another computer and adjust), edit it (remove settings, set permissions), and copy it back as ntuser.man under the C:\Users\\%username%folder. Logon and profit.

Bypasses for Specific Group Policy Settings/Hardening:

**Prevent access to the command prompt and registry editing tools**

The figure below displays the interface for the Group Policy Object editor. If you’re not familiar with with Microsoft and AD GPO, then this is the place you need to head to if you need or want to configure policy enforcement on endpoints. This area can be found under ‘User Configuration > Policies > Administrative Templates > System’. To prevent access to the command prompt and registry editing tools you’ll want to find these two settings and modify them:

* ‘Prevent access to the command prompt’
* ‘Prevent access to registry editing tools’

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/0 (34).png>)

These settings are not just enabled – they have sub-settings as well. On the command prompt setting, we have the ability to choose if we want to disable the command prompt script processing also. The default option is No.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/1 (20).png>)

For registry editing tools, you have the option to disable regedit running silently or not. The default option is Yes.

When these settings are in place, you will get an error if you attempt to run cmd.exe or regedit.exe. Note that it also blocks reg.exe, regini.exe, conhost.exe, and more.

![A screenshot of a computer error

Description automatically generated](<../../.gitbook/assets/2 (19).png>)

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/3 (18).png>)

The bypasses you need are different depending on the settings. Let’s go over how to bypass the command prompt restrictions first.

Scenario 3 – Command Prompt Disabled and Script Processing Enabled

In this scenario, you can do a lot of fun stuff. Every command you want to run can be prefixed with ‘cmd /c or cmd /k.’ For instance, if you want to do a directory listing, you can do ‘cmd/k dir c:\\.’ Or, if you want to output the results to a file instead, you can run ‘cmd /c dir c”\\> c:\temp\dir\_c.txt.’

You don’t get an interactive prompt, but you are still able to get those precious commands executed.

I have also seen in many cases that people forget to think about PowerShell.exe, meaning that you can still start up powershell.exe and use that as an interactive shell. Another option is to use a LOLBin that can execute whatever you want (e.g., forfiles.exe).

Scenario 4 – Command Prompt Disabled and Script Processing Disabled:

This setup makes it more difficult to run commands since we can no longer use /c or /k to execute using cmd.exe. The first step I would try would be to see if you can fire up PowerShell as an alternative. What applies or enforces on the CLI, doesn’t necessarily mean it applies and enforces on PS. If that does not work, another approach is to use a LOLBin that can execute code and does not rely on cmd.exe. For instance, forfiles.exe will be blocked by this setting when script processing is disabled.

Another cool bypass I have used in the past is to use Didier Stevens cmd.exe or cmd.dll. This is a recompiled ReactOS version of the file. The process can be found here: [https://blog.didierstevens.com/my-software/#cmd-dll](https://blog.didierstevens.com/my-software/#cmd-dll)

After you download it, you should be able to run the cmd.exe (unless application allowlisting or some other hardening is getting in your way).

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/4 (18).png>)

In the above figure, you can see that the normal cmd.exe on the left is blocked and the downloaded version works just fine.

Scenario 6 – Registry Editing Tools Disabled and Allowed to Run Silently

You might have guessed that this is easy to bypass since we can execute it silently. Let me go over some examples of how to read and change the registry when this setting is in place. Reading the registry can be done in many ways. One way is to use regedit with the /s switch. This indicates silent operation. If you want to read HKEY\_Current\_User\Environment, you can use this command to dump it to a registry file:

Regedit /s hkey\_current\_user\environment

Afterward, you can open that registry file in Notepad.exe or use type in a command prompt to see the registry values, as seen in the figure below.

![A screenshot of a computer program

Description automatically generated](<../../.gitbook/assets/5 (17).png>)

If you want to write directly to the registry, you can do an import using regedit. That means you have to prepare a .reg key with the desired settings and then you can run:

Regedit /s registryfile.reg

Another useful option is a visual basic script (VBScript). In many cases, you can save the .vbs file and execute it directly from its saved location. The three (3) lines below are all that is needed to read out the path variable from the registry:

Set objWshShell = WScript.CreateObject("WScript.Shell")strKeyToRead = objWshShell.RegRead("HKCU\Environment\path")wscript.echo strKeyToRead

These three (3) lines can be used to write to the registry using a vbscript:

Set objWshShell = WScript.CreateObject("WScript.Shell")myKey = "HKCU\Environment\mysetting"objWshShell.RegWrite myKey,1,"REG\_DWORD"

Scenario 8 – Registry Editing Tools Disabled and Allowed to Run Silently Disabled

In this scenario, we can no longer use regedit /s. If you attempt to execute regedit /s, you will get the same error when executing regedit normally. The vbscript approach will still work since this setting will, in most cases, block native Windows registry editing binaries.

In addition to vbscript, you can also attempt PowerShell. If you want to look inside a registry hive, you can do a CD and ls into it, as shown in the screenshot below.

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/6 (17).png>)

You can also browse the different keys by using CD, as shown in the next screenshot.

![A computer screen shot of a blue screen

Description automatically generated](<../../.gitbook/assets/7 (16).png>)

If you want to look inside HKLM instead, you can use HKLM:. To write a value using PowerShell, you can use the following command:

Set-ItemProperty HKCU:\Environment\test\ -Name ha -Value works

![A blue screen with white text

Description automatically generated](<../../.gitbook/assets/8 (16).png>)

If neither vbscript nor PowerShell can help, I would attempt to download Didier Stevens’ recompiled ReactOS version of regedit. It can be found on his blog here: [https://blog.didierstevens.com/my-software/#regedit-dll](https://blog.didierstevens.com/my-software/#regedit-dll).

When it is downloaded, you can simply run:

rundll32 \<path\_to\_dll>,DllMain

That should then open a Registry Editor, as shown in the screenshot below:

![A screenshot of a computer

Description automatically generated](<../../.gitbook/assets/9 (15).png>)
