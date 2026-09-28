# IR-02: Business email compromise (incident response runbook)

**Trigger:** Forwarding-rule alert (SOC-01), a risky sign-in, or a customer asking about changed bank details (ATK-01)  
**Severity:** P2; P1 if money has moved  
**Example targets:** Contain within 30 minutes of confirmation  
**Framework:** NIST SP 800-61 phases

## 1. Detect and analyse

1. **[L1]** Check the account's sign-ins: new country, new device, attacker IP ranges.
2. **[L1]** Review mailbox activity: inbox rules, sent items, mail read (MailItemsAccessed).
3. **[L1]** Check for new MFA methods and OAuth app consents.

> **Decision:** Were fraudulent payment requests sent?  
> **Yes:** call finance and the affected customers now, and ask the bank to recall payments.  
> **No:** carry on with containment.

## 2. Contain

1. **[L1]** Revoke sessions and block sign-in (SOC-04 automates this after approval).
2. **[IT]** Service desk verifies the user by phone, then resets the password and MFA.
3. **[L1]** Remove the attacker's inbox rules and MFA methods.
4. **[L2]** Block attacker IPs with a Conditional Access named location.

## 3. Eradicate

1. **[L2]** Hunt for the same IPs signing in to other accounts.
2. **[L2]** Remove malicious OAuth apps and purge the original phishing email (SOC-03).

## 4. Recover

1. **[IT]** Re-enable the user with phishing-resistant MFA.
2. **[L1]** Tell the user what happened and what to watch for.
3. **[L1]** Extra monitoring on the account for 30 days.

## 5. After the incident

1. **[DPO]** Assess the mailbox contents for personal data and decide on ICO reporting within 72 hours.
2. **[Mgmt]** Confirm finance calls back on a known number before any bank-detail change.
3. **[L2]** Lessons learned; tune the detections.

Roles: L1 SOC analyst · L2 incident lead · IT operations · DPO data protection officer · Mgmt leadership.

---

Reference design by Archi Rose Mani. Part of the portfolio at [archirose.github.io](https://archirose.github.io). Back to the [index](../README.md).
