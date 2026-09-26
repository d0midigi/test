# LDAP Channel Binding and Signing

### The LDAP Enforcement Era: Server 2025 and Beyond

With Microsoft finally "enforcing" LDAP Signing by default in Windows Server 2025, it is time to revisit the "old friends" of AD hardening: LDAP Channel Binding and LDAP Signing.

Despite years of warnings, many AD environments still lack these configurations. Worse, many organizations haven't even begun the auditing process. If you want to avoid being caught off guard by the new Server 2025 defaults, now is the time to act.

#### TL;DR: What You Need to Know

* Server 2025 Changes: Domain Controllers (DCs) now have LDAP Signing enabled by default via a new policy: `LDAP server signing requirements Enforcement`. It defaults to "Not Configured," which now translates to Require Signing.
* Channel Binding: No change to defaults here; it remains disabled unless you manually configure it.
* The Golden Rule: Audit before you enforce. A 30-day audit period is usually enough to identify legacy applications that might break.

#### What’s New in Server 2025?

Microsoft is aggressively targeting insecure LDAP because it is a primary vector for credential exploitation.

* LDAP Signing: In Server 2025, the default behavior is "Require Signing." To change this, you must explicitly set the new enforcement policy to "Disabled."
* LDAP Channel Binding: This is still completely disabled by default. You should, at a minimum, set this to "When Supported" to begin capturing events.

**The "New-ish" Patch (KB4520412)**

For those on Server 2019 or 2022, a critical update (August 2023) introduced two "What-If" Event IDs to help you test Channel Binding without breaking connectivity:

| **Event ID** | **Description**                                                       |
| ------------ | --------------------------------------------------------------------- |
| 3074         | Client used SSL/TLS but would have failed Channel Binding validation. |
| 3075         | Client used SSL/TLS but did not provide Channel Binding info.         |

#### Deep Dive: Signing vs. Channel Binding

While often grouped together, these are distinct security layers:

**1. LDAP Signing (The Digital Signature)**

* Function: Requires clients to digitally sign requests. This proves the message came from the reported client and hasn't been tampered with.
* Protection: Prevents unauthorized modifications of LDAP messages in transit.
* Implementation:
  * Client Side: Set `Network security: LDAP client signing requirements` to "Require signing".
  * DC Side (Pre-2025): Set `Domain controller: LDAP server signing requirements` to "Require signing".
  * DC Side (Server 2025): Set the old policy to "None" and the new `Enforcement` policy to "Enabled".

**2. LDAP Channel Binding (The Secure Tunnel)**

* Function: Ties the TLS tunnel to the application layer, creating a unique Channel Binding Token (CBT).
* Protection: Specifically designed to stop Relay Attacks.
* Requirement: Only works with LDAPS (LDAP over SSL/TLS, Port 636).
* Implementation: Set `Domain controller: LDAP server channel binding token requirements` to "Always" (Goal) or "When Supported" (Auditing).

#### How to Implement Without Breaking Everything

Don't guess—audit. Follow this 5-step workflow to harden your environment safely:

1. Enable Diagnostics: On all DCs, enable LDAP interface logging:
   * `Reg Add HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics /v "16 LDAP Interface Events" /t REG_DWORD /d 2`
2. Set "When Supported": Configure Channel Binding GPO to "When Supported". This logs failures without blocking them.
3. Monitor Your SIEM: Look for the following Event IDs:
   * 2889: Signing failures.
   * 3074 & 3075: Channel Binding gaps.
4. Remediate: Use the source IP addresses in the logs to find the "offending" legacy apps or non-Windows devices and update their configurations.
5. Enforce: Once the logs are clear, flip the GPOs to "Always" and "Require Signing" (one at a time!).

#### Final Verdict: Defense in Depth

Should you enable Signing if you already use LDAPS? Absolutely. While LDAPS provides encryption, LDAP Signing provides superior protection against relay attacks. Using both creates a robust "defense-in-depth" posture that makes your Active Directory a much harder target for attackers.

Here is a script you can run from a management workstation (with appropriate permissions) to audit your Domain Controllers and enable the necessary diagnostic logging.

#### PowerShell: LDAP Audit & Setup Tool

```powershell
# 1. Define your Domain Controllers
$DCs = Get-ADDomainController -Filter * | Select-Object -ExpandProperty Name

# 2. Enable LDAP Interface Diagnostic Logging (Level 2)
# This allows the capture of Event ID 2889
foreach ($DC in $DCs) {
    Write-Host "Enabling LDAP Diagnostics on $DC..." -ForegroundColor Cyan
    Invoke-Command -ComputerName $DC -ScriptBlock {
        $path = "HKLM:\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics"
        Set-ItemProperty -Path $path -Name "16 LDAP Interface Events" -Value 2
    }
}

# 3. Check for recent "Offending" Events
# This looks for Signing (2889) and Channel Binding (3074, 3075) failures
Write-Host "`nSearching for insecure LDAP binds in the last 24 hours..." -ForegroundColor Yellow

$Events = foreach ($DC in $DCs) {
    Get-WinEvent -ComputerName $DC -FilterHashtable @{
        LogName = 'Directory Service'
        Id = 2889, 3074, 3075
        StartTime = (Get-Date).AddDays(-1)
    } -ErrorAction SilentlyContinue
}

if ($Events) {
    $Events | Select-Object TimeCreated, Id, MachineName, Message | Out-GridView -Title "LDAP Audit Results"
} else {
    Write-Host "No insecure binds detected in the last 24 hours. Keep monitoring!" -ForegroundColor Green
}
```

#### Implementation Roadmap

To help visualize how these settings work together to block attacks, refer to the communication flow below:

#### Next Steps for Remediation

Once you have identified the source IPs from the script above, you should:

1. Update Linux/Unix Clients: Check `sssd.conf` or `ldap.conf` on Linux servers to ensure `ldap_id_use_start_tls = True` and `ldap_tls_cacert` are configured.
2. Appliance Check: For printers or scanners using "Scan to Email," switch the port from 389 to 636 and upload the Root CA certificate to the device.
3. Third-Party Apps: Ensure any application connecting to AD is using a service account with GSSAPI or StartTLS enabled.
