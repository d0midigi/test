---
icon: bone-break
---

# Chapter 89 - AdminSDHolder Abuse, SDProp Manipulation, and Protected-Object Privilege Persistence (Offensive)

### Abstract

Active Directory protects high-value administrative principals through AdminSDHolder and the Security Descriptor Propagator, but the same mechanism can become an unusually durable persistence primitive when an adversary gains control of the protected security descriptor or the objects governed by it. This chapter examines protected-object persistence primarily from the offensive perspective, beginning with protected-group discovery and `adminCount` analysis before progressing through AdminSDHolder ACL manipulation, inherited-permission suppression, SDProp behavior, nested privileged groups, hidden access control entries, object ownership, password-reset authority, group modification, shadow administrative rights, and persistence that can reappear after defenders repair individual accounts. Particular attention is given to the difference between directly modifying a privileged object and modifying the template that repeatedly governs privileged objects. Defensive treatment follows through protected-object inventory, AdminSDHolder baselining, ACL normalization, stale `adminCount` remediation, Tier 0 change monitoring, directory-state comparison, and adversarial validation. The chapter establishes that privileged-object security cannot be trusted when the mechanism responsible for protecting those objects has itself become an attacker-controlled persistence engine.
