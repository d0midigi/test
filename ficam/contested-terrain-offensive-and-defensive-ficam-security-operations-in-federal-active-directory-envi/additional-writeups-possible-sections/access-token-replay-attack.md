# Access Token Replay Attack

* Definition: An attack where a valid access token, captured from a legitimate communication between a client and a server, is "replayed" (resent) by an unauthorized actor to gain access to protected resources.
* Attack Category: Broken Authentication / Improper Session Management.

#### Technical Mechanism

The attack exploits the "stateless" nature of many modern APIs. If a Resource Server (API) only checks if a token is digitally signed and not expired, it has no way of knowing if the person presenting the token is the person it was originally issued to—unless specific "sender-constrained" protections are in place.

#### Prerequisites

1. Token Acquisition: The attacker must be able to intercept or steal a valid, active token.
2. Lack of Sender-Constraining: The token must be a Bearer Token. Like cash, whoever holds a bearer token is "borne" the right to use it.
3. Active Session: The token must not yet be expired or revoked.

#### How It Is Performed

1. Interception: The attacker sniffs the token via a Man-in-the-Middle (MitM) attack, or steals it from the user's browser storage (Local Storage/Session Storage) via Cross-Site Scripting (XSS).
2. Extraction: The attacker extracts the `Authorization: Bearer <token>` string from the HTTP headers.
3. Replay: The attacker sends a new request to the Resource Server, pasting the stolen token into their own header.
4. Access: The server validates the signature, sees the token is "valid," and grants the attacker access.

#### Tool(s) Used

* Burp Suite / OWASP ZAP: To intercept traffic and "Repeater" modules to replay the request.
* Postman: To easily craft API requests with stolen headers.
* Browser DevTools: To manually pull tokens from `LocalStorage`.
* Wireshark: If the traffic is unencrypted (rare today) or if the attacker has decrypted the TLS stream.

#### Impact

* Unauthorized Data Access: Reading sensitive user data, emails, or PII.
* Account Takeover: If the token has scopes for profile modification.
* Privilege Escalation: If the stolen token belongs to an administrator.
* API Abuse: Using the victim's quota or performing actions (like deleting resources) in their name.

#### Detection

* IP Monitoring: Detecting a single token being used from two vastly different geographic locations or IP addresses simultaneously.
* User Agent Anomalies: If a token issued to a Chrome/Windows client is suddenly used by a Python/Linux script.
* Token Usage Patterns: Monitoring for a sudden spike in API calls using a specific token ID (`jti`).

#### Mitigation

* DPoP (Demonstrating Proof-of-Possession): A newer standard that binds a token to a specific private key held by the client.
* mTLS (Mutual TLS): Binds the token to the TLS certificate of the sender.
* Short Expiry Times: Reduce the "window of opportunity" for a replayed token.
* Strict Scopes: Ensure tokens only have the minimum permissions necessary (Principle of Least Privilege).
* Use HttpOnly Cookies: Store tokens in cookies that JavaScript cannot access to prevent theft via XSS.

#### Related Attacks

* Pass-the-Hash: The NTLM equivalent in older Windows environments.
* Session Hijacking: Stealing a session cookie rather than an OAuth token.
* Token Binding: A specific defense mechanism against replay attacks
