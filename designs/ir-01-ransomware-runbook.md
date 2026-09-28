# IR-01: Ransomware on the network (incident response runbook)

**Trigger:** EDR ransomware alert, mass file renames, a ransom note, or shadow copies being deleted (ATK-02)  
**Severity:** P1, critical  
**Example targets:** Confirm in 15 minutes; contain within 1 hour  
**Framework:** NIST SP 800-61 phases

## 1. Detect and analyse

1. **[L1]** Confirm the alert: ransom note, changing file extensions, shadow-copy deletion.
2. **[L1]** Scope it: which devices, accounts and file shares.
3. **[L2]** Declare a P1, open the incident bridge and start the timeline log.

> **Decision:** Is encryption still spreading?  
> **Yes:** isolate the whole segment and disconnect backup targets now.  
> **No:** contain device by device.

## 2. Contain

1. **[L1]** Isolate affected devices in Defender for Endpoint; the EDR stays connected.
2. **[IT]** Disable compromised accounts and take affected shares offline.
3. **[L2]** Block the attacker's IPs, domains and file hashes everywhere.
4. **[L2]** Image memory and disk on the first infected host before any rebuild.

## 3. Eradicate

1. **[L2]** Find the way in (VPN, RDP or phishing) and close it.
2. **[L2]** Remove persistence: new accounts, scheduled tasks, services, GPO changes.
3. **[IT]** Reset privileged credentials, including the KRBTGT account twice.

## 4. Recover

1. **[IT]** Rebuild infected hosts and restore data from backups taken before the compromise.
2. **[IT]** Bring services back in priority order, scanning each restore.
3. **[L1]** Watch restored systems closely for 30 days.

## 5. After the incident

1. **[DPO]** Decide on reporting to the ICO within 72 hours if personal data is at risk.
2. **[Mgmt]** Report the crime: Police Scotland on 101, or Action Fraud in England, Wales and Northern Ireland. Tell the NCSC about significant incidents.
3. **[L2]** Lessons-learned review within two weeks; add detections for anything missed.

Roles: L1 SOC analyst · L2 incident lead · IT operations · DPO data protection officer · Mgmt leadership. Any ransom decision sits with leadership and legal advisers, not the SOC.

---

Reference design by Archi Rose Mani. Part of the portfolio at [archirose.github.io](https://archirose.github.io). Back to the [index](../README.md).
