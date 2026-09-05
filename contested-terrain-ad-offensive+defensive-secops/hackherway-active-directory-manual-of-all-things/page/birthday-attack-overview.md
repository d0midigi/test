# Birthday Attack Overview

### Birthday Attack Overview

In a birthday attack, an attacker abuses a security feature: hash algorithms, which are used to verify the authenticity of messages. The hash algorithm is a digital signature, and the receiver of the message checks it before accepting the message as authentic. If a hacker can create a hash that is identical to what the sender has appended to their message, the hacker can simply replace the sender’s message with their own. The receiving device will accept it because it has the right hash.

The name “birthday attack” refers to the birthday paradox, which is based on the fact that in a room of 23 people, there is more than a 50% chance that two of them have the same birthday. Hence, while people think their birthdays, like hashes, are unique, they are not as unique as many think.

To prevent birthday attacks, use longer hashes for verification. With each extra digit added to the hash, the odds of creating a matching one decrease significantly.
