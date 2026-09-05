# Brute Force Attacks Overview

### Brute-Force Attacks Overview

A brute-force attack gets its name from the “brutish” or simple methodology employed by the attack. The adversary simply tries to guess the login credentials of someone with access to a target system. Once they get it right, they are in.

While this may sound time-consuming and difficult, adversaries often use bots to crack the credentials. The adversary provides the bot with a list of credentials that they think may give them access to the secured area. The bot then tries to each one while the adversary sits back and waits. Once the correct credentials have been entered, the adversary gains access.

To prevent brute-force attacks, have lockout policies in place as part of your authorization security architecture. After a certain number of attempts, the user attempting to enter the legitimate credentials gets locked out. This typically involves “freezing” the account so even if someone else tries from a different device with a different IP address, for example, they cannot bypass that lockout.

It is also wise to use random passwords without the use of regular words, dates, or sequences of numbers in them. This is effective because, for example, even if an adversary uses software to try to guess a 10-digit password, it will take many years of non-stop attempts to get it right.
