<h1>Chapter X: AD CS - The PKI Highway to Domain Admin</h1>
<h2><i>Abusing Certificate Templates for Instant Persistence and Escalation</i></h2>
<h3>X.1 The Hidden Power of PKI in Active Directory</h3>
* **The Certificate Authority (CA):** How the CA functions as a "Shadow Domain Controller."
* **The Enrollment Process:** A technical breakdown of how a "Principal" requests a certificate and how the CA validates it.
* **Terminology for Defenders:** Understanding CSRs (Certificate Signing Requests) and X.509 extensions.

<h3>X.2 Identifying "Juicy" Misconfigurations (ESC1 - ESC8)</h3>
* **Template Analysis:** Using `Certify` , `Certipy`, or `Cerebrate` to find misconfigured templates.
* **The "Golden" Flaw (ESC1):** When `ENROLLEE_SUPPLIES_SUBJECT` is enabled - allowing any user to impersonate a Domain Admin.
* **Manager Approval Bypasses:** Abusing templates that don't require authorized signatures.

<h3>X.3 The Attack Path: From User to Administrator</h3>
* **Requesting the Certificate:** The command-line logic/syntax for requesting a certificate for a fake identity.
* **The PFX Handshake:** Converting a certificate into a Kerberos TGT (Ticket Granting Ticket) using the Rubeus tool.
* **Persistence:** How attackers use long-lived certificates to maintain access even after password resets, OS wipes and reboots.

<h3>X.4 Blue Team: Monitoring and Auditing PKI</h3>
* **The "Smoking Gun" Logs:** Monitoring Event ID 4886 (Certificate request received) and 4887 (Certificate issued).
* - **Subject Alternative Name (SAN) Alerting:** Why you must alert whenever a certificate is issued where the requester differs from the Subject Name.
- **The PKI Audit:** Using the `PSPkiAudit` PowerShell module to find vulnerabilities before attackers do.

**7.5 Remediation: Closing the Certificate Gaps**

- **Template Hardening:** Disabling the `CT_FLAG_ENROLLEE_SUPPLIES_SUBJECT` flag.
- **Permission Cleanup:** Removing "Authenticated Users" from the enrollment rights of sensitive templates.
- **Modern Defense:** Moving toward **Windows Hello for Business** and hardware-backed keys.

<h2>Use This "Researcher Prompt" to Write This Section</h2>
Since AD CS attacks are complex, use this prompt with a model like **DeepSeek-R1** or **GPT-4o** to get the content for this section:
**Prompt:** "I am writing the 'ESC1' section of my AD CS chapter. Act as an AD Security Auditor. Explain the technical danger of the `'ENROLLEE_SUPPLIES_SUBJECT'` flag in a Certificate Template. Specifically, explain how an attacker provides a **Subject Alternative Name (SAN)** to the CA to receive a certificate for a Domain Administrator. Provide the **PowerView** command to find these templates and the **Rubeus** command to use the resulting certificate for a Kerberos exchange. Format this as a 'Technical Deep-Dive' for a professional textbook."
