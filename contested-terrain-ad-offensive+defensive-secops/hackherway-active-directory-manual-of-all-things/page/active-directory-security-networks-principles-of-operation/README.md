# Active Directory Security Networks Principles of Operation

This section outlines how the IEEE 802.11 Robust Security Network (RSN)s operate and how they integrate with enterprise identity systems such as Active Directory (AD). It starts with the frame-exchange sequence that creates an association (5.1), then surveys the RSN frame types and the layout of data frames. A five-phase lifecycle of RSN operation is introduced at a high level in 5.2, while 5.3-5.7 dive into each phase. In Enterprise networks, RSNs rely on AD-backed RADIUS servers during the authentication phase (typically Phase 2) to validate user or device credentials via 802.1X, mapping the 802.11 association to an AD account and applying Group Policy. For a concise overview, read the opening of 5.1 and all of 5.2, skim the remainder of Section 5, and finish with the summary in 5.8.

<a href="../../" class="button primary">1. STA → AP: Association Request → The probe-response phase is already complete, so the STA now asks to join the BSS whose SSID is "NotSecure."</a>



````
```html
<div style="border-left:4px solid #2196F3;padding:12px 16px;margin:16px 0;background:#e3f2fd;color:#0d47a1;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,Arial,sans-serif;font-size:14px;line-height:1.5;">
  <strong>ℹ️ Info:</strong> 802.11 Association vs. RSN Authentication<br>
  The exchange shown here only creates a <strong>record</strong> that the STA is reachable at this AP.
  Security keys are <strong>not</strong> derived until the 802.1X/EAP handshake (backed by Active Directory via RADIUS) completes later.
  Until then, the STA is associated but <strong>not</strong> admitted to the RSN.
</div>
```
````

{% hint style="info" %}
1. STA → AP: Association Request\
   The probe-response phase is already complete, so the STA now asks to join the BSS whose SSID is "NotSecure."
2. AP → STA: Association Response\
   The AP creates a per-STA association table entry that maps the STAs MAC to its current BSSID and returns Success (or a rejection reason).
{% endhint %}

At this point, the STA is "associated," but no keys exist and no user identity has been proved. The AP simply knows where to deliver downstream frames. In an RSN the next step is 802.1X/EAP, and in an Active Directory-based Enterprise that EAP conversation is relayed by the AP to a RADIUS server that ultimately checks the credentials hash against AD.
