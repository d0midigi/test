# Credential Prediction Attack

Credential/Session Prediction Attack

\### Credential/Session Prediction

Credential/Session Prediction is a technique used to hijack or impersonate a web site user by deducing or guessing the unique value that identifies a particular session or user. Also known as Session Hijacking, this attack allows attackers to issue web site requests with the compromised user's privileges.

Most web sites authenticate and track users when communication is first established. Users typically prove their identity by supplying a username/password combination. Instead of passing these credentials with each transaction, web sites generate a unique "session ID" to identify the user session as authenticated. Subsequent communication is tagged with the session ID as "proof" of the authenticated session. If an attacker can predict or guess another user's session ID, they can perform fraudulent activities.

\*\*Example\*\*

Many web sites generate session IDs using proprietary algorithms, which might be as simple as incrementing static numbers or involve more complex procedures like factoring in time and other computer-specific variables. The session ID is stored in a cookie, hidden form-field, or URL. If an attacker can determine the algorithm used to generate the session ID, they can mount an attack as follows:

1\. The attacker connects to the web application and acquires the current session ID.

2\. The attacker calculates or brute forces the next session ID.

3\. The attacker switches the current value in the cookie/hidden form-field/URL and assumes the identity of the next user.
