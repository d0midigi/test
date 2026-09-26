# Common Roadblocks Encountered by Attackers

This scenario describes a shift from "brute-force" tactics to a much more sophisticated "identity-provider" attack. When an attacker pivots from a local Active Directory (AD) breach to compromising the Active Directory Federation Services (ADFS), they move from trying to guess keys to essentially becoming the locksmith.

The transition from a local network breach to a full cloud compromise represents a critical escalation in modern cyber warfare. While a local breach of Active Directory (AD) provides an attacker with a treasure trove of NTLM hashes, the utility of those hashes is often stalled by the realities of modern defensive architecture. In a legacy environment, those hashes might allow for lateral movement via Pass-the-Hash (PtH) techniques, but the cloud is a different beast. Services like Azure or AWS do not typically accept local NTLM hashes for authentication; they require modern protocols that are often guarded by the "steel door" of Multi-Factor Authentication (MFA).

For the sophisticated adversary, attempting to crack thousands of high-entropy passwords or tricking hundreds of employees into approving MFA prompts is an inefficient use of time and increases the risk of detection. Instead, they shift their focus toward the architecture of the trust itself. This leads them to the Active Directory Federation Services (ADFS), the critical gateway that translates local identities into cloud-compatible assertions. By targeting the federation provider, the attacker stops acting like a thief trying to pick a lock and starts acting like the locksmith who manufactured the door.

The core of this strategy lies in the exploitation of the SAML (Security Assertion Markup Language) protocol. ADFS serves as the "Identity Provider" (IdP), and cloud services act as "Service Providers" (SP). When a user wants to access a cloud resource, ADFS issues a digitally signed SAML token that tells the cloud service exactly who the user is and what they are allowed to do. The security of this entire ecosystem rests upon a single cryptographic pillar: the Token Signing Certificate. If an attacker has already compromised the on-premises AD, they can often pivot to the ADFS server, extract this private key, and use it to sign their own fraudulent SAML assertions.

This technique, famously known as a "Golden SAML" attack, offers a level of access that is virtually indistinguishable from legitimate traffic. Because the attacker is signing the tokens themselves, they can forge a claim that explicitly states "MFA has already been performed." To the cloud service, this token looks perfectly valid and fully authenticated. The attacker can effectively impersonate any user in the organization—from the CEO to the Global Administrator—without ever knowing their actual password or needing to touch their physical phone or hardware security key.

The implications of this breach extend far beyond the Microsoft ecosystem. While Microsoft 365 and Azure are the most common targets, ADFS is frequently used as a central hub for a sprawling web of third-party integrations. This "Federated Identity" model is designed for convenience, allowing a single set of credentials to grant access to a vast array of enterprise tools. Once the federation provider is compromised, the "blast radius" encompasses every service that trusts those SAML assertions. This includes critical infrastructure components like Amazon Web Services (AWS) or Google Cloud Platform, where an attacker could spin up rogue resources or exfiltrate massive databases.

Furthermore, this access penetrates deep into the business operations layer. Critical platforms such as the SAP Enterprise Portal, Salesforce, and ServiceNow become open books. Even bespoke business-to-government (B2G) applications or proprietary B2B portals used for supply chain management are brought into scope. The attacker essentially gains a "skeleton key" to the company’s entire digital existence. Because this method bypasses the standard authentication logs that would flag a failed password attempt or an ignored MFA prompt, the adversary can maintain a persistent, silent presence across the entire corporate landscape for as long as that signing certificate remains valid.

#### The Limitation of Traditional Credential Theft

In a traditional breach, an attacker may possess the NT LAN Manager (NTLM) hashes for every user in the company. However, the path to the cloud is often blocked by two major hurdles:

1. Cracking Latency: High-entropy passwords can take weeks or months to crack, or may be impossible with current resources.
2. MFA Blockades: Even with a cleartext password, a prompt for a hardware key, biometric, or push notification usually halts the attack in its tracks.

For an attacker, this is a "low-probability" game. They need a "high-probability" strategy that bypasses the user’s credentials entirely.

### The Power of the Federated Pivot

Instead of attacking the user, the sophisticated attacker attacks the Trust Relationship.

ADFS acts as the bridge between your on-premises network and the cloud. It uses the Security Assertion Markup Language (SAML) to tell cloud services, "I have verified this user; you can let them in."

#### Why This Strategy Is Superior

By compromising the ADFS server—specifically the Token Signing Certificate and its private key—the attacker gains the ability to forge SAML tokens. This technique, often called Golden SAML, offers three devastating advantages:

* Bypassing MFA: Because the cloud service (like Azure/M365) trusts ADFS to handle authentication, a forged token looks like a "completed" login. The cloud service assumes MFA was already performed on-premises and lets the attacker in instantly.
* Password Irrelevance: The attacker never needs to know the user's password. They simply sign a piece of data that says "This is the CEO," and the cloud accepts it as truth.
* Persistent Stealth: These forged tokens can be generated for any user at any time, making it incredibly difficult for security teams to detect "impossible travel" or unauthorized access through standard logs.

### Expanding the Blast Radius: Beyond Microsoft

The danger of a compromised Federation Provider isn't limited to Outlook or Teams. Modern enterprises use ADFS as a Single Sign-On (SSO) hub for their entire ecosystem.

When the Federation "source of truth" is compromised, the "blast radius" expands to include:

| **Sector**                   | **Examples of At-Risk Services**                           |
| ---------------------------- | ---------------------------------------------------------- |
| Cloud Infrastructure         | Amazon Web Services (AWS) consoles, Google Cloud Platform. |
| Enterprise Resource Planning | SAP Enterprise Portal, Oracle Cloud.                       |
| CRM & Sales                  | Salesforce, HubSpot.                                       |
| Operations & HR              | ServiceNow, Workday, BambooHR.                             |
| Custom Apps                  | Bespoke B2B portals or B2G (Government) applications.      |

In this scenario, the attacker doesn't just "breach the network"—they inherit the digital identity of the entire organization. They can pivot from a local workstation to a global AWS administrator account without ever typing a single password.

The transition from a compromised internal network to a full-scale federation breach is a calculated evolution of an attack. Once an adversary has established a foothold, their primary objective is to identify high-value targets that facilitate persistence and privilege escalation. In a modern Windows environment, the presence of Active Directory Federation Services (ADFS) stands out as a lighthouse. Despite its critical role in global identity management, an ADFS host is essentially a Windows Server running specific role-based services. If an attacker has already performed a full directory dump of the Active Directory, they likely possess the administrative credentials or service account hashes necessary to access these hosts. While interacting with these servers does leave a forensic trail—such as event logs related to service access or anomalous logins—the payoff for the attacker far outweighs the risk of discovery.

To successfully execute a "Golden SAML" attack, the adversary must extract two specific pieces of cryptographic material from the ADFS environment. The first is the X.509 Token Signing Certificate. This certificate is the digital identity of the ADFS server itself; it is the "stamp of authority" that proves to any external application that the authentication response is legitimate. However, the certificate alone is inert without its corresponding Private Key. This key is typically protected by the Distributed Key Management (DKM) service, which stores the sensitive data in a specific container within Active Directory. By leveraging their previous AD compromise, the attacker can decrypt this private key. Once they possess both the certificate and the key, they effectively own the organization’s identity supply chain, allowing them to forge authentication responses that bypass passwords and MFA entirely.

The feasibility of this exploit is rooted in the fundamental architecture of modern federated authentication. In Microsoft's ecosystem, a "Relying Party Trust" is established between the ADFS (the Identity Provider) and an external application (the Service Provider). This relationship is built on a "set it and forget it" trust model. When a user attempts to log into a service like Salesforce or Office 365, the application recognizes that it is not the authority for that user's credentials. It then redirects the user's browser to the ADFS server. This redirection is a crucial point of failure in a compromise scenario because the process is asynchronous. The application essentially hands the user off to the ADFS server and waits for them to return with a "receipt" of successful login; it has no visibility into what happens during the ADFS interaction.

During this "blind spot" in the workflow, the ADFS server is solely responsible for challenging the user, verifying their password, and confirming their MFA status. The Relying Party remains entirely dormant and uninvolved. It only re-enters the conversation once the user returns with a SAML response. Because the application cannot see the ADFS server's internal process, it relies entirely on the cryptographic signature attached to that response. It uses the public portion of the ADFS certificate—exchanged during the initial setup of the trust—to verify that the response was signed by the "real" ADFS server.

This inherent trust is what makes the spoofing of responses so devastating. If an attacker uses the stolen private key to sign a forged SAML assertion, the application has no technical way to distinguish it from a legitimate one. The forged token can explicitly include claims stating that the user has successfully passed an MFA challenge, even if the attacker doesn't have a phone or hardware key paired to the account. The application, acting as the Relying Party, "trusts" that the ADFS server did its due diligence. Since the signature is mathematically valid, the application grants full access to the attacker, leaving the victim organization completely unaware that the "secure" perimeter of their identity provider has been turned against them.

To understand why the asynchronous nature of this process is a "crucial point of failure," it helps to think of the application (the Relying Party) as a high-security building and the ADFS server as a third-party notary office across town.

When you try to enter the building, the security guard says, "I don’t know you. Go to the notary on Main Street, get a signed letter proving who you are, and come back." At that moment, the guard stops watching you. They don't follow you to the notary, they don't watch the notary check your ID, and they don't witness the notary signing the paper. They simply wait for you to return.

#### The "Blind Spot" in the Workflow

In technical terms, this redirection creates a total lack of state or oversight between the application and the Identity Provider (IdP). Because the process is asynchronous, the application "forgets" about the user the moment the redirect command is sent. It has no live connection to the ADFS server to monitor the authentication attempt.

This creates a massive security vacuum that an attacker can exploit in several ways:

* Lack of Direct Verification: The application does not call the ADFS server via a back-channel to ask, "Hey, did you just see Bob Smith?" Instead, it sits passively and waits for the user's browser to deliver a SAML token.
* Trust in the "Receipt" only: The application is programmed to trust the _artifact_ (the signed token) rather than the _process_. It assumes that if a token arrives and the digital signature is mathematically valid, then all the necessary steps—like checking a password or verifying a hardware MFA key—must have happened correctly.
* The Forgery Window: Because the application is not an active participant in the authentication, it cannot tell the difference between a token generated by a legitimate ADFS server and one generated by an attacker sitting in a coffee shop using a stolen private key. As long as the attacker can sign the "receipt" with the stolen key, the application accepts it as absolute truth.

#### The "Out of Band" MFA Fallacy

The asynchronous nature of the protocol is also why MFA fails to protect the cloud resource once the ADFS server is compromised. In a healthy environment, ADFS would pause the login to demand a mobile push notification. However, because the application is just waiting for a signed token to appear, an attacker can simply write a line of code into their forged token that says `AuthnContext: MultipleFactorAuthentication`.

The application sees this claim, sees the valid signature, and assumes the MFA "transaction" happened while the user was away at the "notary." It has no way to verify if a text message was ever sent or if a biometric was ever scanned.

#### Why This is the "Point of Failure"

In a synchronous or direct authentication model (like logging directly into a database with a username and password), the server is an active participant in the handshake. It sees the attempt, it controls the challenge, and it validates the response in real-time.

In the asynchronous federated model, the application abdicates all responsibility for the "how" of authentication. It only cares about the "result." By stealing the keys to the ADFS server, the attacker controls the result, making the entire previous security architecture—no matter how many firewalls or MFA layers were in place—completely irrelevant.

In the context of network security and ADFS, calling a process asynchronous means that the two parties involved—the Application (Relying Party) and the ADFS server (Identity Provider)—do not maintain a live, constant connection with each other while the user is logging in. They are essentially "talking past each other" through the user's web browser.

To understand why this is a massive security gap, it helps to look at the difference between a Synchronous (Direct) conversation and an Asynchronous (Indirect) hand-off.

#### The Synchronous Model (The Direct Connection)

In a traditional, synchronous login—like when you log into a local Windows computer—the computer asks for your password and immediately checks its own database to see if it’s correct. The "question" and the "answer" happen in one continuous, locked-down session. The computer is an active participant in every millisecond of that transaction. If anything looks wrong, the computer knows instantly because it is the one conducting the test.

#### The Asynchronous Model (The "Hand-Off")

In the ADFS world, the process is broken into disconnected segments. The Application and the ADFS server never actually "speak" to one another directly during the login. Instead, they use the user's browser as a middleman to pass messages back and forth.

Here is how that "asynchronous" breakdown works in practice:

1. The Abandonment: When you click "Login" on an application like Salesforce, the application sends a "Redirect" command to your browser. At that exact moment, the application drops the connection. It doesn't follow you to the ADFS page, and it doesn't "watch" what you do there. It essentially goes to sleep regarding your session.
2. The Isolated Authentication: You are now at the ADFS server. The ADFS server does its job—asking for your password or MFA. But because the process is asynchronous, the ADFS server isn't reporting back to the application in real-time. It’s working in a vacuum.
3. The "Receipt" Delivery: Once ADFS is satisfied, it gives your browser a signed SAML Token (the "receipt"). Your browser then carries that receipt back to the application.
4. The Blind Acceptance: The application "wakes up" when your browser hits its URL again. It doesn't ask the ADFS server, "Hey, did you actually see this guy?" Instead, it just looks at the digital signature on the receipt. If the signature matches the key it has on file, it assumes everything that happened while it was "asleep" was legitimate.

#### Why "Asynchronous" is the Attacker's Best Friend

The "point of failure" occurs because the application is relying on a piece of paper (the token) rather than a live witness. In a synchronous system, an attacker would have to trick the server while it is actively watching. In this asynchronous system, the attacker realizes they don't need to go to the ADFS server at all. If they have stolen the private "signing pen" (the Token Signing Certificate) from the ADFS server, they can sit in a dark room, manufacture a fake "receipt" that says "This user is the Admin and they passed MFA," and sign it themselves.

When the attacker presents that fake receipt to the application, the application checks the signature and says, "This looks like it was signed by the ADFS server I trust. I wasn't there to see the login happen, but the paperwork is in order, so come on in."

Because the process is asynchronous, there is no out-of-band verification. The application has no way to cross-reference the token with a "live" login event. It is the ultimate "don't ask, don't tell" policy of the internet, and it's exactly what allowed major breaches like the SolarWinds/Nobelium attack to go undetected for so long.

The leap from simply "being on the network" to "owning the identity provider" is facilitated by specialized tooling designed to exploit the very way Windows handles service secrets. One of the most prominent tools for this is ADFSDump. To use it effectively, an attacker cannot simply run it as a standard administrator; they must execute the .NET runtime within the specific security context of the ADFS Service Account.

In a well-architected environment, ADFS is configured to use a dedicated service account to limit the "blast radius" of a compromise. The primary goal of this requirement is to protect the Distributed Key Management (DKM) container within Active Directory. The DKM is a highly restricted storage area that holds the private keys used to unlock the encrypted Token Signing Certificates. Under best practices, even a Domain Administrator is theoretically barred from accessing these keys—only the ADFS service account itself should have the "Read" permissions necessary to retrieve them. By impersonating this account, the attacker bypasses these intended hurdles, extracting the "key to the keys."

When ADFSDump is executed successfully, it reveals the inner sanctum of the federation service. A typical output will display multiple decryption keys, often labeled as "Private Keys," alongside an encrypted version of the Token Signing Key. The attacker’s task is to identify the correct master private key, which is then used to peel back the encryption on the Token Signing Key. Once this cryptographic material is in the attacker’s hands, they have everything they need to sign their own digital "passports" to any service the company uses.

Beyond just stealing keys, ADFSDump also exfiltrates the "blueprints" of the organization’s trust network: the Relying Party Trusts. This metadata is invaluable because it tells the attacker exactly what information a specific application (like AWS, Salesforce, or Office 365) expects to see in a login token. Without this, an attacker might forge a validly signed token that still fails because it is missing a specific "claim"—a piece of data like a user’s employee ID or their specific department. By reviewing the trusts for utilities like ClaimsXray or the Office 365 Identity Platform, the attacker learns the exact dialect each application speaks.

The true engine of ADFS is its Claims-Based Authentication model. This system uses "Claim Rules" to transform raw directory data into specific attributes that an external application can understand. For an attacker, these rules are a roadmap for privilege escalation. For example, a rule might be set up to look for any Active Directory group starting with the prefix `AWS-` and map that group directly to a high-privileged IAM role in the Amazon cloud. By identifying these mapping schemes, an attacker can craft a spoofed response that doesn't just say "I am a user," but specifically says "I am a user with the 'AWS-Cloud-Admin' role," granting them immediate, high-level access upon login.

To put this into action, attackers often use intercepting proxies like Burp Suite. This "person-in-the-middle" tool allows them to pause the conversation between their browser and the cloud service, modifying the data on the fly. The attack begins innocently enough: the attacker goes to the Microsoft 365 login page and enters a target's email address. Microsoft’s backend recognizes that the domain (e.g., `@tokelosh.net`) is federated and redirects the browser to the organization's ADFS server.

At this stage, the ADFS server would normally demand a password and an MFA prompt. However, the attacker completely ignores the ADFS server's requests. Instead, they use a tool like ADFSpoof to manually generate a WS-Fed or SAML response using the cryptographic keys they stole earlier. This spoofed response is a pre-packaged "success" message. Using Burp Suite, the attacker intercepts the traffic and swaps the legitimate (but incomplete) authentication attempt with their perfectly crafted, digitally signed forgery.

When this forged response reaches Microsoft 365, the cloud service performs a single check: "Is this message signed by the certificate I have on file for this company?" Because the attacker used the actual private key from the ADFS server, the math checks out perfectly. Microsoft 365 has no way of knowing the ADFS server was never actually involved in the login. It accepts the token as absolute truth, and the attacker is instantly logged in as the victim user, gaining full access to their emails, files, and administrative powers without ever needing to know a single password.

####

####
