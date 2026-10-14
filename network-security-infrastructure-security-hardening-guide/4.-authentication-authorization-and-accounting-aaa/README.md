# 4. Authentication, Authorization, and Accounting (AAA)

Authentication, Authorization, and Accounting (AAA) Centralized AAA (Authentication, Authorization, and Accounting) servers offer a consolidated system for managing administrative access to devices. User accounts created through these servers are more secure against compromise because credentials are not stored directly on the devices. Proper configuration of AAA servers establishes an authoritative source for managing and monitoring access, enhances consistency in access control, reduces configuration maintenance, and lowers administrative costs. It is recommended to configure all devices to utilize modern AAA services. Here's an example configuration command for Cisco IOS devices:

```bash
aaa new-model
```

Implementing the above configuration ensures that devices do not rely on legacy authentication and authorization methods, thereby enhancing security and compliance with modern standards.
