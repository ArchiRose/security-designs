# ATK-01: Phishing to mailbox takeover

**Scenario:** Business email compromise against a Microsoft 365 tenant  
**Framework:** MITRE ATT&CK (Enterprise)

Each step shows what the attacker does, the control that prevents it, and the detection that catches it if prevention fails.

| # | Tactic | Technique | Attacker | Prevent | Detect |
|---|---|---|---|---|---|
| 1 | Initial access | `T1566.002 Spearphishing Link` | Emails a link to a fake Microsoft 365 sign-in page. | Safe Links checks the link at click time (ARC-04). Staff know the report button. | User reports it; a tenant-wide hunt finds every recipient (SOC-03). |
| 2 | Credential access | `T1557 Adversary-in-the-Middle · T1539 Steal Web Session Cookie` | A proxy page relays the real sign-in and steals the session cookie, which gets past ordinary MFA. | Phishing-resistant MFA and compliant devices (ARC-02). | Entra ID Protection flags an anomalous token or unfamiliar sign-in. |
| 3 | Initial access | `T1078.004 Valid Accounts: Cloud Accounts` | Signs in as the user from the attacker's own infrastructure. | Conditional Access blocks sign-ins from unmanaged devices. | Sign-in from a new country or hosting provider. |
| 4 | Persistence | `T1098.005 Device Registration` | Registers their own MFA method to come back later. | Security info can only be registered from trusted locations or compliant devices. | Alert on new MFA methods in the Entra ID audit log. |
| 5 | Defence evasion · Collection | `T1564.008 Email Hiding Rules · T1114.003 Email Forwarding Rule` | Adds an inbox rule that hides replies and forwards finance email out. | External auto-forwarding blocked by the outbound spam policy. | SOC-01 forwarding-rule detection. |
| 6 | Impact | `T1657 Financial Theft` | Emails customers new bank details from the real mailbox. | Finance calls back on a known number before any bank-detail change. | Customer or bank query. Contain with SOC-04 and runbook IR-02. |

**Response:** Contain with SOC-04 and follow runbook IR-02.

---

Reference design by Archi Rose Mani. Part of the portfolio at [archirose.github.io](https://archirose.github.io). Back to the [index](../README.md).
