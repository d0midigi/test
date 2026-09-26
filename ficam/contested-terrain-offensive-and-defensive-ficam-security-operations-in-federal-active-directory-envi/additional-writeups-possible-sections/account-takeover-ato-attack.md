# Account Takeover (ATO) Attack

* Definition: A form of identity theft where an attacker successfully gains unauthorized access to a victim's online account (e.g., banking, email, social media, or e-commerce) and changes the credentials or settings to lock out the legitimate owner and perform fraudulent activities.
* Attack Category: Identity Theft / Fraud / Unauthorized Access.

#### Technical Mechanism

The mechanism varies based on the method, but the core goal is to bypass the Authentication Layer. This is done by either stealing existing credentials, exploiting a flaw in the "Forgot Password" logic, or bypassing Multi-Factor Authentication (MFA). Once inside, the attacker typically changes the associated email address and password to "homestead" the account.

#### Prerequisites

1. Identity Data: The attacker needs a starting point, such as a username, email address, or phone number.
2. Weak Authentication: The target account typically lacks robust MFA or uses easily guessable/leaked passwords.
3. Vulnerable Recovery Flow: A "Forgot Password" process that relies on insecure methods (like SMS or easily researched security questions).

#### How It Is Performed

1. Credential Stuffing: Using massive lists of leaked usernames/passwords from previous data breaches on other sites, hoping the victim reused their password.
2. Phishing/Smishing: Tricking the user into entering their credentials on a fake login page.
3. Session Hijacking/Fixation: Stealing active session cookies to "jump" into a logged-in state without needing a password.
4. SIM Swapping: Redirecting the victim's phone number to the attacker's SIM card to intercept SMS-based MFA codes.
5. Brute Force: Systematically guessing passwords (though this is often caught by modern "account lockout" policies).

#### Tool(s) Used

* Sentry MBA / SilverBullet: Popular tools for automated credential stuffing and web testing.
* Evilginx2: A sophisticated framework used for "Man-in-the-Middle" phishing to bypass MFA in real-time.
* Burp Suite: Used to manipulate requests during the "Forgot Password" or "Change Email" flows.
* The Dark Web: To purchase "Combolists" (lists of leaked credentials) and "Logs" (stolen browser data from info-stealer malware).

#### Impact

* Financial Loss: Direct theft from bank accounts or unauthorized purchases on e-commerce sites.
* Reputational Damage: Sending spam or malicious links to the victim's contacts.
* Data Ransom: Holding a high-value account (like an Instagram handle or gaming account) for ransom.
* Secondary Attacks: Using the hijacked email as a "base of operations" to reset passwords for every other account linked to it.

#### Detection

* Impossible Travel: Login attempts from two different countries within a short timeframe.
* Velocity Checks: Multiple failed login attempts in a short period from the same IP or targeting the same user.
* Device Fingerprinting: Detecting a login from a new device, browser, or operating system that the user has never used before.
* Immediate Profile Changes: Security alerts triggered when an email or password is changed immediately after a login from a new IP.

#### Mitigation

* Hardware Security Keys: Using FIDO2/WebAuthn keys (like YubiKeys) which are virtually immune to phishing.
* Authenticator Apps: Moving away from SMS-based MFA to TOTP (Time-based One-Time Password) apps.
* Password Managers: Encouraging unique, complex passwords for every single service to prevent credential stuffing.
* Risk-Based Authentication: Implementing systems that require extra verification if the login looks "suspicious" (e.g., different location).

#### Related Attacks

* Business Email Compromise (BEC): A high-stakes version of ATO targeting corporate executives.
* Social Engineering: Manipulating customer support agents to grant access to an account.
* Adversary-in-the-Middle (AiTM): Phishing attacks that intercept both passwords and MFA codes simultaneously.
