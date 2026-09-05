# Network Attacks and Defense

The demand for security professionals who understand how attackers compromise networks is increasing daily. News articles frequently highlight incidents of ransomware or personal information being stolen from unprotected databases. In response to these ever-growing cyberattacks and threats that plague organizations and companies daily, the United States has established an organization dedicated solely to countering these cyber threats and attacks. Both public and private companies depend on skilled professionals to conduct test attacks on their networks to identify vulnerabilities before attackers do. These professionals are often referred to as ethical hackers, security testers, or penetration testers.

This chapter is not designed to provide comprehensive training in security or penetration testing. Instead, it introduces security testing to newcomers in the field. It is intended for novices with a solid foundation in computer and networking basics who want to learn how to protect networks by using an attacker’s perspective to identify and mitigate security risks. By understanding the tools and methods hackers use to breach networks, security testers can better protect systems from these attacks.

The aim of this book is to help you become a proficient security tester. This profession demands creativity and critical thinking, skills that can be challenging to develop in a traditional academic setting; however, with an open mind and a willingness to learn, you can start thinking outside the box and asking more questions than this book or instructor might pose. Solving complex problems requires patience and the ability to accept that sometimes there isn’t a simple answer.

Conducting a security test involves more than just running exploits against a system and informing your client of the vulnerabilities found. It’s crucial to consider whether you might have missed testing certain areas that could be vulnerable to attacks. Haphazard approaches can undermine the security profession and leave companies exposed to threat. This course aims to provide a more structured approach to conducting security tests and to introduce novices to the professional certifications available in this growing field.

**Intended Audience**

This book is designed specifically for those with, at a minimum, a Security+ or Network+ certifications or equivalent knowledge. A solid understanding of networking is essential to grasp how computers function within a networked environment and to collaborate effectively with network administrators. Additionally, readers should be proficient in using a computer from the command line and familiar with popular operating systems like Windows and Kali Linux.

**Chapter Descriptions**

This book is organized into fourteen comprehensive chapters, each addressing key aspects of ethical hacking, network security foundations, and cybersecurity fundamentals.

**Chapter 1: Ethical Hacking Overview** introduces the legal boundaries of an ethical hacker’s activities, outlines the roles of security and penetration testers, and reviews the latest certifications available at the time of this publication.

**Chapter 2: TCP/IP Concepts Review** explores the layers of the TCP/IP protocol stack, highlights important ports, and covers IP addressing along with binary, octal, and hexadecimal numbering systems.

**Chapter 3: Network and Computer Attacks,** learners examine the various types of malicious software, methods for protecting against malware attacks, different network attack techniques, and aspects of physical security.

**Chapter 4: Footprinting and Social Engineering** examines the use of web tools for footprinting, techniques for gathering competitive intelligence, DNS zone transfers, and social engineering strategies.

**Chapter 5: Port Scanning** explains the different types of port scans, demonstrates how to use port scanning tools, conducts ping sweeps, and illustrates how to use shell scripting to automate security tasks.

**Chapter 6: Enumeration** focuses on the steps and tools required for enumerating operating systems, including both Windows and UNIX/Linux environments.

**Chapter 7: Programming for Security Professionals,** the chapter provides an overview of programming concepts relevant to network and computer security, equipping readers with the necessary coding skills to enhance their security practices.

**Chapter 8: Desktop and Server OS Vulnerabilities** discusses vulnerabilities specific to Windows and Linux systems and outlines best practices for hardening computers and servers running these operating systems.

**Chapter 9: Embedded Operating Systems: The Hidden Threat** explains what embedded operating systems are, their common applications, known vulnerabilities, and best practices for protecting these systems.

**Chapter 10: Hacking Web Servers** covers web applications and their vulnerabilities, as well as the tools used to attack web servers, enabling readers to understand and mitigate web-based threats.

**Chapter 11: Hacking Wireless Networks,** learners receive an overview of wireless technologies, and IEEE wireless standards, and study wireless authentication methods, wardriving techniques, and both offensive and defensive wireless hacking tools.

**Chapter 12: Cryptography and Encryption** provides a comprehensive summary of the history and principles of cryptography and encryption, explains various encryption algorithms and components of Public Key Infrastructure (PKI), and offers examples of different attacks on cryptosystems.

**Chapter 13: Network Protection Systems** covers a variety of devices used to protect networks, including routers, firewalls, and intrusion detection and prevention systems, ensuring that readers understand how to implement effective network defense.

This structured approach ensures that readers gain a thorough understanding of both theoretical concepts and practical skills necessary for effective ethical hacking and cybersecurity.

**Key Features**

This book is designed with several features to enhance your understanding of computer and network security:

* **Chapter Objectives:** Each chapter starts with a detailed list of key concepts you need to master, serving as a quick reference to the chapter’s content and as a helpful study aid.
* **Figures and Tables:** Screenshots will guide you through using security tools, including command-line utilities, and program creation. Diagrams will help you to better visualize important concepts, while tables present information in an organized, easy-to-understand manner.
* **Hands-On Activities:** To reinforce your learning, practice exercises are embedded throughout each chapter, giving you the chance to apply the tools and techniques used in network security and testing.
* **Notes:** Helpful notes throughout the book provide additional material related to the subject at hand. Special “Bytes and Bits of Knowledge” notes offer real-world examples that relate directly to security topics discussed in each chapter.
* **Tips:** Extra information on resources and problem-solving strategies is provided though tips to enhance your learning experience.
* **Caution Icons:** These warnings alert you to potential mistakes or issues, along with advice on how to avoid them.
* **Chapter Summary:** At the end of each chapter, a summary will review the key concepts, providing a useful tool for revisiting and consolidating your understanding of key concepts and topics covered.
* **Key Terms:** Important terms introduced throughout the chapters are highlighted in bold and gathered in a key terms list at the end of each chapter. Each key term is fully defined in the Glossary, promoting a deeper understanding of the chapter’s content.
* **Review Questions:** To help you assess your grasp of the material, each chapter concludes with review questions that reinforce the key concepts and techniques covered.
* **Case Projects:** Finally, each chapter ends with case projects that challenge you to apply what you’ve learned in real-world scenarios. These projects often involve a hypothetical company similar to those that hire security consultants, requiring you to combine technical knowledge and practical problem-solving skills.

By incorporating these features, this book ensures a comprehensive and engaging learning experience, preparing you to tackle real-world challenges in computer and network security.

The hands-on activities in this course are designed to help you apply your knowledge of security and penetration testing. To complete these activities, you'll need to meet the following system requirements:

\- \*\*Computers\*\*: Each computer should be capable of booting to Windows 10 or later.

\- \*\*Internet Access\*\*: Ensure that each computer is connected to the internet and configured to receive IP configuration via DHCP from a router.

\- \*\*Kali Linux\*\*: You'll need Kali Linux for various hands-on activities. This can be in the form of a live bootable version on a USB drive, a virtual machine, or a computer with a full Kali Linux OS installation.

**Operating Systems and Hardware**

The activities involving Windows were primarily designed for Windows 10, but they should also work on Windows 11. The computers should meet these minimum specifications:

* **Kali Linux from USB:** If you're using a USB flash drive to run Kali Linux, your PC must support USB booting, and the drive should have at least 8 GB of storage with a minimum read/write speed of 15 MB/second.
* **Video Card:** A video card with 512 MB of video RAM.
* **Hard Drive:** 80 GB of hard drive space.
* **Processor:** A 1.5 GHz 32-bit or 64-bit processor.
* **System RAM:** 8 GB of RAM.
* **Wireless Card:** Required for some optional wireless activities.
* **Input Devices:** A mouse or other pointing device, along with a keyboard.

**Security-Testing Tools**

Throughout the book, you'll engage in activities that require various security tools. These tools are available as freeware, shareware, or free versions for home and educational use. Since URLs can change frequently, use a search engine to find any tools if the listed URLs are no longer valid. Additionally, you'll need Microsoft Office Word (or another word processor) and email software installed on your computer.

**The Kali Linux Operating System (OS) Distribution**

Kali Linux is integral to many hands-on activities in this book, and you have several options for setting it up:

* **Virtual Machine Installation:** You can install Kali Linux as a virtual machine using free virtualization software like VMware Server or VirtualBox. This option allows you to run Kali Linux alongside Windows, providing the convenience of using both operating systems simultaneously.
* **USB Flash Drive Installation:** Another option is to install Kali Linux on a USB flash drive with at least 8 GB of storage. This approach lets you carry your customized Linux environment and use it on any compatible system, with the added benefit of saving files and reports directly on the drive.
* **Dual-Boot Installation:** If you prefer, you can set up Kali Linux in a dual-boot configuration with Windows. This method allows you to choose between the two operating systems at startup; however, the dual-boot process can be more complex, especially if you're using BitLocker or other disk encryption tools. Although this book doesn't cover dual-boot installation, you'll find plenty of online resources to guide you.
* **Full Installation on Hardware:** You can also install Kali Linux directly on your computer as the sole operating system. If you choose this method, be careful not to overwrite any existing operating systems.

**Creating a Bootable USB Flash Drive**

To install Kali Linux on a USB flash drive, you'll need a drive with at least 8 GB of capacity. Keep in mind that the speed of some flash drives may not be sufficient for running a live Linux OS. For better performance, it's recommended to use a flash drive with a minimum read and write speed of 15 MB/second. Faster drives can significantly improve the overall experience. You can check performance benchmarks on sites like \[https://usb.userbenchmark.com]\(https://usb.userbenchmark.com) to help you select a suitable drive within your budget.

Once you've chosen the right flash drive, refer to the \[Kali Linux website]\(https://www.kali.org/docs/usb/) for the most up-to-date USB installation instructions. The site provides step-by-step guidance for users on Windows, Linux, or macOS, covering everything from downloading Kali Linux to booting into it for the first time. After installation, ensure your Kali Linux software is up to date by running the apt-get update and apt-get upgrade commands to check for any available updates in the Kali Linux repositories.

**Installing New Software**

Since Kali is a Debian-based Linux distribution, you have access to thousands of free programs that can be easily downloaded and installed using a few simple commands. These programs are stored in online archives known as repositories, which are specific to your operating system version. To install new software, you can use the command apt-get install packagename, replacing "packagename" with the name of the software you wish to install. If you're unsure of the exact package name, you can use a search engine to find it.

**Community Support for Kali Linux**

For the latest Kali Linux updates and access to online forums where you can find help with troubleshooting, visit https://www.kali.org. This site is an excellent resource if you're looking to learn more about Kali Linux and stay up to date with the latest developments.
