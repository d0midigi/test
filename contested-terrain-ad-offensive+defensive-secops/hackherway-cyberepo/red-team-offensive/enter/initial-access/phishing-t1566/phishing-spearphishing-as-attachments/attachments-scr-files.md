# Attachments: SCR Files

SCR files are specialized files designed for Windows as screensavers to help save energy. These screensavers activate when there is no user activity for a set period of time, typically containing Portable Executable (PE) files with an .scr extension. The system's defaulot screensaver application, scrnsave.scr, can be found in the directories C:\Windows\System32 and C:\Windows\sysWOW64 on 64-bit versions of Windows. Screensaver configurations are stored in the Registry under HKCU: Control Panel\Desktop\ and can be adjusted for persistent use.

Various tools like msfvenom, Phantom Evasion, and Veil Framework can be utilized to generate binary payloads for customization. By altering the file extension of an executable created with msfvenom from .exe to .scr, it can be disguised as a screensaver file. Despite the change in extension, the functionality of the payload remains unaffected, enabling comparison with the original payload.

For this scenario, I plan to use a basic payload generated with the msfvenom tool, saving it as an EXE file. By changing the file extension to .scr on the Attacker machine, we can compare both payloads. Despite the altered extension, the functionality remains unchanged.

<figure><img src="../../../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

I will transfer these files to our Windows Box so we can observe the subtle yet significant difference. Upon examination, we will note that the description information for the EXE file identifies it as an Application, while the SCR file is labeled as a Screensaver. This distinction is advantageous as it can potentially deceive our target into believing the SCR file is just a typical Screensaver File.



<figure><img src="../../../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

If we look at the Processes list, we can see our payload running.

<figure><img src="../../../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

We can also see the SCR file in the list, as well:

<figure><img src="../../../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

The reason for the same results is that SCR extensions are also executable on a Windows machine. To enhance the credibility of the file and increase the likelihood of it being opened, we can take further steps. This includes spoofing the extension and switching the icon to make it appear more authentic and convincing.



<figure><img src="../../../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

By spoofing the extension and switching the icon to a more innocuous image, we can create the impression that the file is a harmless image rather than an executable; however, in reality, the file is still a malicious executable that will enable us to establish a connection back to our attacking machine. This deception tactic can increase the chances of the file being opened and executed by the target.
