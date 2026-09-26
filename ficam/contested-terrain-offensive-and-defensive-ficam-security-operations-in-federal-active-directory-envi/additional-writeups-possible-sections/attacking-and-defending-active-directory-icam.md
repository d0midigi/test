# Attacking and Defending Active Directory ICAM

Securing and attacking Active Directory (AD) ICAM is essentially a high-stakes game of "Capture the Flag" where the flag is Domain Admin access. Attackers use techniques like Kerberoasting or Pass-the-Hash to move from a standard user to a god-like administrator. Defenders, meanwhile, use Tiered Administration and Zero Trust principles to ensure that even if one account is compromised, the "Keys to the Kingdom" remain out of reach.

1. AD ICAM Fundamentals: The structure and protocols (how the "engine" works).
2. The Attacker's Playbook: Reconnaissance and finding the "weak links."
3. Escalating Privileges: Turning a regular user into a powerhouse.
4. Domain Dominance: Techniques for taking total control (and staying there).
5. The Defensive Fortress: Building a modern, tiered defense.

#### Step 1: AD ICAM Fundamentals

To defend or attack anything, you first have to understand how it's built. Think of Active Directory (AD) as the "City Hall" of a corporate network. It stores all the identities (users), credentials (passwords), and access rules (who can enter which building).\
ICAM stands for Identity, Credential, and Access Management. In AD, this is organized in a hierarchy:

* Forest: The entire city.
* Domain: A specific neighborhood.
* Organizational Units (OUs): Specific houses or apartment blocks where users and computers live.

**The Goal of ICAM:** To make sure that when "Alice" tries to log in, she is actually Alice (Identity), her password is correct (Credential), and she is allowed to read the "Secret Project" folder (Access).\
Fun Fact: If you’re a Domain Admin, you’re basically the mayor, the police chief, and the person who owns all the master keys. If an attacker "becomes" you, the city is effectively theirs.<br>
