# CN-002: Anonymous Network Logon from CLIENT1

| Field | Value |
| --- | --- |
| Alert | Anonymous network logon (Event 4624), 1 event |
| Date | 10/25/2026 5:13 PM |
| Host | DC1 |
| Account | NT AUTHORITY\ANONYMOUS LOGON (S-1-5-7) |
| Verdict | **Benign** |
| Escalate | No |

## How I found it

While baselining which accounts make network logons (Type 3) on DC1, every account matched a known machine or user except one ANONYMOUS LOGON.

```
index=windows EventCode=4624 Logon_Type=3 | stats count by Account_Name | sort -count
index=windows EventCode=4624 Account_Name="ANONYMOUS LOGON"
```

## What I checked

- **Logon Type 3** from **CLIENT1 (192.168.10.20)**, a known domain computer on the lab network
- **Elevated Token: No**: the session had no admin rights
- **Authentication Package NTLM, Package Name NTLM V1**. NTLMv1 is weak and normally worth flagging, but anonymous sessions send no password and are labeled NTLM V1 by Windows. NTLMv1 audits exclude ANONYMOUS LOGON for this reason.
- Single event, not repeated, no other suspicious activity around it

## Verdict

Benign: a routine anonymous lookup from a known domain computer.

## Escalation

No. I would escalate if anonymous logons came from an unknown IP, repeated in volume, or if a named user account showed NTLM V1.

## Lesson

An indicator only means something in context. NTLM V1 for a real user is a finding; NTLM V1 for ANONYMOUS LOGON is expected.

| | |
| --- | --- |
| Accounts with network logons | ![](../screenshots/06-splunk-searches/10-accounts-network-logons.png) |
| Event detail | ![](../screenshots/07-investigations/03-anonymous-logon-event.png) |
| Network information | ![](../screenshots/07-investigations/04-anonymous-logon-network-info.png) |
| Authentication | ![](../screenshots/07-investigations/05-anonymous-logon-ntlm.png) |
