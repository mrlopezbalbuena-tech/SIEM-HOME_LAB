# Windows Logon Types and Event IDs

## Logon types (Events 4624 / 4625)

| Type | Name | Meaning | Red flag |
| --- | --- | --- | --- |
| 0 | System | Windows at startup | Rare |
| 2 | Interactive | At the keyboard | Admin console logins at odd hours |
| 3 | Network | Over the network (shares, GPO, AD) | Many failures from one IP |
| 4 | Batch | Scheduled task | Unknown scheduled tasks (persistence) |
| 5 | Service | Service started | New service with a strange name |
| 7 | Unlock | Screen unlocked | Rare |
| 8 | NetworkCleartext | Password sent in plain text | Exposed passwords |
| 9 | NewCredentials | runas /netonly | Credential-theft tools |
| 10 | RemoteInteractive | Remote Desktop (RDP) | RDP from unknown or outside IPs |
| 11 | CachedInteractive | Cached credentials, DC unreachable | Rare |

## Key Security Event IDs

| ID | Event |
| --- | --- |
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4634 / 4647 | Logoff |
| 4648 | Logon with explicit credentials |
| 4672 | Admin privileges assigned at logon |
| 4688 | New process started |
| 4720 | User account created |
| 4724 | Password reset attempt |
| 4728 / 4732 / 4756 | Member added to a security group |
| 4740 | Account locked out |
| 4768 / 4769 | Kerberos ticket requested |
| 4776 | NTLM credential validation |
| 7045 | New service installed (System log) |
| 1102 | Security log cleared |

## Failed logon Sub Status codes

| Code | Meaning |
| --- | --- |
| 0xC000006A | Valid username, wrong password |
| 0xC0000064 | Username does not exist |
| 0xC0000234 | Account locked out |
| 0xC0000072 | Account disabled |
| 0xC0000193 | Account expired |
| 0xC0000071 | Password expired |
