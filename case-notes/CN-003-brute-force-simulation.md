# CN-003: Brute Force with Successful Logon (Tabletop Simulation)

> **This was a tabletop exercise.** The ticket and search results were simulated to practice the triage and escalation process. The host FS01, the account jramirez and the IP below are not real systems in my lab. 203.0.113.0/24 is a documentation-only IP range.

| Field | Value |
| --- | --- |
| Ticket | INC0047213: Excessive failed logons |
| Severity | Medium, **raised to High** |
| Host | FS01 (file server) |
| Account | LAB\jramirez |
| Verdict | **Likely account compromise** |
| Escalate | **Yes** |

## Timeline (10/27/2026)

| Time | Event |
| --- | --- |
| 1:58:04 AM | First failed logon (4625) |
| 2:12:47 AM | Last failed logon, 23 failures total |
| **2:13:15 AM** | **Successful logon (4624), Logon Type 3** |

## What I checked

```
index=windows EventCode=4625 Account_Name=jramirez
index=windows EventCode=4624 Account_Name=jramirez Source_Network_Address=203.0.113.45
```

- All 23 failures and the success came from **203.0.113.45**, a single **external** IP (not a private range)
- **Sub Status 0xC000006A**: the username is valid and the password was wrong, so the attacker knew a real username
- **Logon Type 3** (network); Elevated Token: No

## Verdict

Likely account compromise: a successful brute force from the internet against a file server.

## Recommended actions

1. Disable LAB\jramirez and reset the password
2. Block 203.0.113.45 at the firewall
3. Review what the session accessed on FS01 after 2:13 AM
4. Check whether 203.0.113.45 targeted other accounts or hosts
5. Find out why FS01 accepts logons from the internet
6. Confirm with jramirez that the activity was not theirs

## Lessons

- Start from the ticket's facts: account, host, time window.
- First question: where did it come from? Second: did it succeed?
- A success after many failures means escalate fast and raise severity.
- Recommendations should be specific actions, not general urgency.
