# 2.7 Attack Paths Rather Than Isolated Vulnerabilities

Traditional vulnerability management naturally encourages analysis at the level of individual findings.

A host is missing a patch. A protocol is enabled. An account has a weak password. A permission is overly broad. A certificate template is misconfigured. A service is exposed. Each condition is identified, assigned severity, documented, and remediated independently.

That approach remains necessary, but it is incomplete for identity infrastructure.

Identity compromise frequently develops through combinations of conditions whose individual severity appears modest.

A user may possess permission to modify an otherwise unimportant group. That group may control another group. The second group may administer a server. An administrator may maintain an active session on that server. The attacker may obtain the administrator's credential material and use it against a more sensitive system.

No single relationship necessarily looks like domain compromise when viewed alone.

Together they form a path.

Attack-path analysis shifts the emphasis from isolated weakness to reachable authority.
