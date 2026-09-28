# ATK-02: Ransomware through exposed remote access

**Scenario:** Human-operated ransomware against a Windows network  
**Framework:** MITRE ATT&CK (Enterprise)

Each step shows what the attacker does, the control that prevents it, and the detection that catches it if prevention fails.

| # | Tactic | Technique | Attacker | Prevent | Detect |
|---|---|---|---|---|---|
| 1 | Initial access | `T1133 External Remote Services · T1110.003 Password Spraying` | Password spray against the VPN or an exposed RDP server. | No RDP on the internet; MFA on the VPN. | SOC-01 rule: many failures, then a success from the same IP. |
| 2 | Execution | `T1059.001 PowerShell` | Runs encoded PowerShell to download tools. | Attack surface reduction rules; PowerShell script block logging on. | SOC-01 rule: PowerShell with an encoded command. |
| 3 | Credential access | `T1003.001 LSASS Memory` | Dumps passwords and hashes from memory. | Credential Guard; the ASR rule that blocks credential theft from LSASS; LAPS for local admin. | Defender alert on LSASS access. |
| 4 | Lateral movement | `T1021.001 RDP · T1021.002 SMB/Windows Admin Shares` | Spreads to servers with the stolen admin account. | Segmented network (ARC-03); separate admin accounts; no workstation-to-workstation SMB. | Admin logons from unusual hosts (Event 4624, logon types 3 and 10). |
| 5 | Defence evasion | `T1562.001 Disable or Modify Tools` | Tries to switch off antivirus and EDR. | Defender tamper protection. | Tamper-attempt alerts. |
| 6 | Impact | `T1490 Inhibit System Recovery · T1486 Data Encrypted for Impact` | Deletes shadow copies, then encrypts file shares. | Immutable, offline backups with tested restores. | Shadow-copy deletion commands (query below); mass file renames. Respond with IR-01. |

**Response:** Respond with runbook IR-01.

## Detection for step 6

```kql
// Shadow copies or backups being deleted: a common last step before encryption (T1490)
DeviceProcessEvents
| where TimeGenerated > ago(1h)
| where FileName in~ ("vssadmin.exe", "wmic.exe", "wbadmin.exe", "bcdedit.exe")
| where ProcessCommandLine contains "delete shadows"
     or ProcessCommandLine contains "shadowcopy delete"
     or ProcessCommandLine contains "delete catalog"
     or ProcessCommandLine contains "recoveryenabled no"
| project TimeGenerated, DeviceName, AccountName, ProcessCommandLine
```

---

Reference design by Archi Rose Mani. Part of the portfolio at [archirose.github.io](https://archirose.github.io). Back to the [index](../README.md).
