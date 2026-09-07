---
icon: block-brick
---

# Chapter 18 - Group Policy, Configuration Authority, and Enterprise Control

### Abstract

Group Policy converts directory authority into configuration authority across Windows endpoints, servers, and domain controllers. A single Group Policy Object can alter authentication behavior, local privilege, services, firewall rules, audit policy, scripts, registry state, software execution, and security controls across large populations of systems. This chapter examines Group Policy architecture, Group Policy Containers and Templates, SYSVOL, processing order, inheritance, enforcement, security filtering, WMI filtering, loopback processing, client-side extensions, preferences, delegation, software deployment, and policy replication. Offensive analysis focuses on identifying principals capable of editing, linking, owning, or indirectly controlling GPOs and using legitimate policy mechanisms to create privilege, execution, persistence, credential exposure, or defensive impairment. Defensive analysis emphasizes delegation boundaries, Tier 0 policy isolation, baseline enforcement, change monitoring, policy provenance, drift detection, and attack-path reduction. The chapter treats enterprise configuration systems as part of the identity control plane: whoever can alter policy applied to privileged systems may possess authority equivalent to administering those systems directly.



##
