# Appendix X: Advanced Audit Policy Configuration & SIEM Ingestion Guide

* A exact breakdown of which Windows Event IDs must be logged to accurately detect identity attacks (e.g., Event ID 4768/4769 for Kerberos tickets, 4624 for logons).
* Includes recommended SIEM correlation rules and thresholds.
* Preferable to use Splunk Query Language (`sql`) and Kusto Query Language (`kql`) for SIEM rules. YARA will also work.
