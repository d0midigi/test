Microsoft Entra Tenant-User Application Self-Registration



Risk Summary

Custom-developed applications might pose a threat to your environment. A threat actor might use an application to access data in the tenant on behalf of a user. 



Severity: High 



Platform: Entra ID



Category: Infrastructure, Tenant-wide 



MITRE ATT\&CK Tactics: Persistence, Privilege Escalation



MITRE D3FEND Tactics: Application Configuration Hardening 



Description

Custom-developed applications might pose a threat to your environment. A threat actor might use an application to access data in the tenant on behalf of a user. It is recommended to prevent regular users from registering their own applications and let administrators review and register applications. This ensures that the application undergoes a security review before exposing the tenant’s data to the application. 





Real-World Scenario

An employee is phished and consents to a rogue OAuth app that the attacker registered using a standard user account. The app requests Mail.Read and Offline Access, quietly harvesting messages and refresh tokens. The attacker pivots by adding additional permissions and multi-tenant access, enabling persistence beyond the user’s password reset. Finance data is exfiltrated via Graph API with benign-looking traffic, avoiding obvious sign-in anomalies. Defensive strategies need to include detecting risky tenant configurations especially where regular users are allowed to register apps, and raises an alert before widespread abuse. 



Remediation Steps

Follow these steps to remove the vulnerability:



To prevent users from registering their own applications:



) In the Microsoft Entra admin center, go to the User settings section under Microsoft Entra ID.

) Change Users can register applications to No.



How to Prevent It

You can proactively detect and alert on Microsoft Entra tenant where regular users can register applications. It continuously monitors Active Directory, Entra ID, Microsoft 365, and Intune for over 200 misconfigurations, providing early warning before attackers can exploit them. 



FAQ



Why is allowing regular users to register applications a security risk?



How can malicious applications maintain access even after a user resets their password?



What permissions are most commonly abused by rogue applications?



How does Cayosoft Guardian detect when regular users can register applications?



How does Cayosoft Guardian help control OAuth and app-based attack paths?



References



Microsoft Entra admin center – User settings: https://entra.microsoft.com/#blade/Microsoft\_AAD\_IAM/ActiveDirectoryMenuBlade/UserSettings 



Final Thought

Proactive monitoring and timely remediation of configuration risks is essential to maintaining a secure Active Directory and Microsoft 365 environment. By addressing issues like Microsoft Entra tenant where regular users can register applications, you reduce attack surfaces and strengthen your organization’s overall security posture. 





