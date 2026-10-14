# Links: HTA Files

An HTML Application (HTA) program is used as a Microsoft Windows application that combines HTML, Dynamic HTML, and scripting languages supported by Internet Explorer, such as VBScript or JScript.

Given the assumption that email attachments are not allowed, a direct link is shared with the user to download the payload. This method bypasses email security measures and allows the user to access the payload via the provided link.

For instance, a simple script can be created to generate an HTA file that will execute a PowerShell command. This file is then added directly to the link provided to the user. When the user clicks on the link, the browser will recognize the HTA file and execute the embedded PowerShell code.

The effectiveness of this method lies in the ability to bypass email security restrictions and deliver the payload to the target user for execution.

<figure><img src="../../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

By saving the file with a HTA extension, we are able to utilize it as a tool to be sent to our target for execution. It is important to note that such techniques require user interaction, as they need to be opened by the individual; therefore, when crafting a phishing email, it is necessary to provide a compelling reason for the recipient to open the file.

To execute this scheme, we set up a web server and embed the file in our email as an attachment.&#x20;

{% hint style="info" %}
This technique can be categorized as attachment phishing. The key distinction lies in the fact that our attachment doesn't contain executable code; instead, it hosts our link.
{% endhint %}

When the target accesses our email or opens the file, they will find a link embedded in the body of the message. I have chosen to place the email body in an attachment to demonstrate another method of utilizing attachments to include links. It is common practice to include references or links in documents such as PDF files, so this method can be effective in appearing seemingly innocuous to the unsuspecting recipient.

<figure><img src="../../../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Once the target clicks on the link within the email attachment, they may receive prompts or warning messages from their system or browser. These messages typically serve as a security measure to alert the user of potential risks associated with opening unknown files or links.

To persuade the target to proceed with opening the link despite these warning messages, we must provide a convincing excuse or reason. One effective approach could be to frame the link as crucial information or urgent action required, prompting the target to overlook the warnings in favor of accessing what is perceived as important content.

Another approach could be to create a sense of urgency or importance surrounding the link, suggesting that failure to open it promptly could result in negative consequences or missed opportunities. By appealing to the target's curiosity, fear of missing out, or desire for information, we increase the likelihood that they will disregard the warnings and proceed with opening the link.

Ultimately, the success of this phishing technique relies on manipulating the target's emotions and perceptions to justify their decision to bypass the warning messages and access the link provided. By employing persuasive tactics and crafting a compelling narrative, we can increase the chances of the target falling for the phishing attempt and inadvertently exposing themselves to potential risks.

<figure><img src="../../../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

After the target clicks "OK" to proceed past any warning messages or prompts, the payload embedded in the link will be executed on the target machine without any issues. This seamless execution is a critical component of the phishing attack, as it allows the malicious code to run undetected on the target's system.

Upon executing the payload, the attacker gains unauthorized access to the target machine, enabling them to carry out a variety of malicious activities. These activities may include stealing sensitive data, installing malware, monitoring the target's activity, or even taking control of the target machine remotely.

The successful execution of the payload underscores the importance of social engineering in phishing attacks. By persuading the target to click past warnings and prompts, the attacker can exploit the target's trust and willingness to follow instructions, ultimately leading to the compromise of their system and potentially putting their sensitive information at risk.

<figure><img src="../../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

When attempting to execute a .hta (HTML Application) file, the target may encounter a warning message due to the potential security risks associated with downloading and running this type of file. This warning message serves as a safeguard to alert the user about the potential dangers of executing an untrusted or malicious file on their system.

To convince the target to proceed with downloading and executing the .hta file despite the warning, we need to craft a convincing pretext or excuse. One approach could be to frame the file as necessary for accessing important information or completing a task, prompting the target to overlook the warning in favor of obtaining the purported benefits of opening the file.

Additionally, we could create a sense of urgency or importance surrounding the .hta file, suggesting that failure to download and run it promptly could result in negative consequences or missed opportunities. By leveraging psychological triggers such as fear of missing out or the desire for immediate gratification, we increase the likelihood that the target will disregard the warning and proceed with opening the file.

<figure><img src="../../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Then we successfully get a Reverse Shell on our Attacking Machine.

<figure><img src="../../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

It is crucial to highlight the importance of understanding and implementing advanced techniques to create undetectable payloads when engaging in cybersecurity practices such as penetration testing or ethical hacking. While the basic examples discussed in our previous conversation serve as a starting point for familiarizing oneself with common attack vectors and security vulnerabilities, it is essential to recognize that adversaries and security systems are continuously evolving.

As Windows and other operating systems enhance their detection capabilities and security measures, attackers must adapt their tactics to bypass these defenses effectively. Techniques such as obfuscation, encryption, payload manipulation, and other advanced evasion strategies can help attackers create more sophisticated and undetectable payloads that evade detection by security tools and systems.

By investing time and effort in researching and implementing advanced evasion techniques, individuals can enhance their offensive security skills, improve their success rate in bypassing security measures, and better prepare themselves for real-world scenarios where adversaries may employ sophisticated tactics to compromise systems.

Additionally, ethical considerations and adherence to legal and ethical guidelines are essential when performing security assessments or penetration testing. It is crucial to obtain proper authorization and consent before conducting any security assessments and to ensure that all actions taken adhere to ethical standards and legal requirements.

By continuously learning, practicing, and refining their skills in cybersecurity, individuals can stay ahead of emerging threats, enhance their defensive capabilities, and contribute to a safer and more secure cyberspace for all users.
