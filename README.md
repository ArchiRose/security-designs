# Security designs

Reference designs of the kind a SOC or security team works from:

- **architecture** shows how the pieces fit together
- **attack and defence** follows how an attack runs and where it gets stopped
- **threat models** list what could go wrong in a system
- **runbooks** say what to do when it does

These are reference designs I have written up for my portfolio. They do not describe any employer's environment.

Portfolio: [archirose.github.io](https://archirose.github.io). The detections and playbooks that go with them are in [sentinel-soc-automation](https://github.com/ArchiRose/sentinel-soc-automation).

| ID | Design | Type |
|---|---|---|
| ARC-01 | [Microsoft Sentinel SOC architecture](designs/arc-01-sentinel-soc-architecture.md) | Architecture |
| ARC-02 | [Zero Trust sign-in with Conditional Access](designs/arc-02-zero-trust-conditional-access.md) | Architecture |
| ARC-03 | [Network segmentation for a small office](designs/arc-03-network-segmentation.md) | Architecture |
| ARC-04 | [Email security layers](designs/arc-04-email-security.md) | Architecture |
| ATK-01 | [Phishing to mailbox takeover](designs/atk-01-phishing-to-mailbox-takeover.md) | Attack and defence |
| ATK-02 | [Ransomware through exposed remote access](designs/atk-02-ransomware-remote-access.md) | Attack and defence |
| TM-01 | [Small business Microsoft 365 tenant](designs/tm-01-m365-tenant-threat-model.md) | Threat model |
| TM-02 | [Customer file-upload portal](designs/tm-02-file-upload-portal-threat-model.md) | Threat model |
| IR-01 | [Ransomware on the network](designs/ir-01-ransomware-runbook.md) | IR runbook |
| IR-02 | [Business email compromise](designs/ir-02-business-email-compromise-runbook.md) | IR runbook |
| IR-03 | [Malware alert on an endpoint](designs/ir-03-malware-alert-runbook.md) | IR runbook |

## How they connect

- **ARC-01** is the Sentinel architecture that the detections in [sentinel-soc-automation](https://github.com/ArchiRose/sentinel-soc-automation) run on.
- **ATK-01** (phishing to mailbox takeover) is prevented by **ARC-02** (Conditional Access) and **ARC-04** (email security), detected by the SOC-01 rules, and handled with runbook **IR-02**.
- **ATK-02** (ransomware) is slowed by **ARC-03** (segmentation) and handled with runbook **IR-01**.
- **TM-01** threat-models the same Microsoft 365 tenant that **ARC-02** and **ARC-04** protect.

## Frameworks used

MITRE ATT&CK (Enterprise) for attack steps, STRIDE for threat models, NIST SP 800-61 for incident response phases. UK reporting duties appear where they apply: ICO within 72 hours for reportable personal data breaches, and Police Scotland or Action Fraud for cybercrime.

## Licence

Text and diagrams: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Reuse them with credit.
