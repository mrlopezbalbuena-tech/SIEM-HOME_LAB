# Screenshots

Evidence from every stage of the lab build, in the order it happened. Problems are included on purpose: each one is explained in the [troubleshooting log](../docs/04-troubleshooting-log.md).

## 1. Ubuntu Server install

| | |
| --- | --- |
| Keyboard layout | ![](01-ubuntu-install/01-keyboard-layout.png) |
| **Problem:** default disk gave `/` only 11.5 GB | ![](01-ubuntu-install/02-default-disk-only-11gb-root.png) |
| Disk enlarged to 60 GB, but `/` still used half | ![](01-ubuntu-install/03-disk-enlarged-confirm-screen.png) |
| Free space menu | ![](01-ubuntu-install/04-free-space-menu.png) |
| Mounting `/` at full size | ![](01-ubuntu-install/05-mount-root-filesystem.png) |
| Server name and user | ![](01-ubuntu-install/06-profile-setup.png) |
| Skipped Ubuntu Pro | ![](01-ubuntu-install/07-skip-ubuntu-pro.png) |
| Enabled OpenSSH server | ![](01-ubuntu-install/08-enable-openssh.png) |
| No extra snaps | ![](01-ubuntu-install/09-featured-snaps-none.png) |
| Install complete | ![](01-ubuntu-install/10-install-complete.png) |
| First login | ![](01-ubuntu-install/11-first-login.png) |
| System updated | ![](01-ubuntu-install/12-apt-upgrade-complete.png) |

## 2. Networking

| | |
| --- | --- |
| Lab VMs in VirtualBox | ![](02-networking/01-virtualbox-lab-vms.png) |
| Splunk server address (`ip a`) | ![](02-networking/02-ip-a-address.png) |
| NAT Network settings | ![](02-networking/03-natnetwork-settings.png) |
| **Problem:** network can't change while a VM uses it | ![](02-networking/04-natnetwork-change-failed-while-running.png) |
| **Problem:** `ping: command not found` | ![](02-networking/05-ping-command-not-found.png) |
| Typo while installing ping | ![](02-networking/06-iputils-typo.png) |
| ping installed | ![](02-networking/07-iputils-ping-installed.png) |
| VM adapter on the NAT Network | ![](02-networking/08-adapter-on-natnetwork.png) |
| **Problem:** port forwarding pointed outside the network range | ![](02-networking/09-port-forwarding-ip-mismatch.png) |

## 3. Splunk Enterprise install

| | |
| --- | --- |
| Installer downloaded | ![](03-splunk-install/01-splunk-deb-downloaded.png) |
| Installing | ![](03-splunk-install/02-dpkg-installing.png) |
| Install complete | ![](03-splunk-install/03-install-complete.png) |
| **Problem:** service name is case-sensitive (`Splunkd`) | ![](03-splunk-install/04-service-name-case-sensitive.png) |
| Service started | ![](03-splunk-install/05-systemctl-start-splunkd.png) |
| Splunk Web login | ![](03-splunk-install/06-splunk-web-login.png) |
| `windows` index settings | ![](03-splunk-install/07-windows-index-settings.png) |

## 4. Universal Forwarder on Windows Server

| | |
| --- | --- |
| Installer and inputs.conf | ![](04-forwarder/01-installer-and-inputs-conf.png) |
| **Problem:** Splunk IP typed in the Deployment Server box | ![](04-forwarder/02-deployment-server-mistake.png) |
| Forwarder was already installed | ![](04-forwarder/03-already-installed.png) |
| Forwarder connected to 10.0.2.3:9997 | ![](04-forwarder/04-forward-server-active.png) |
| `start` vs `restart` | ![](04-forwarder/05-start-vs-restart.png) |
| **Problem:** index had 0 events | ![](04-forwarder/06-index-zero-events.png) |
| **Cause:** file saved as `inputs.conf.txt` | ![](04-forwarder/07-inputs-conf-txt-extension.png) |
| Events arriving, but "in 3 hours" (time zone) | ![](04-forwarder/08-events-arriving-3-hours-ahead.png) |

## 5. Domain controller DNS and time

| | |
| --- | --- |
| **Problem:** time sync had no data | ![](05-dc1-dns-and-time/01-w32tm-resync-no-time-data.png) |
| Time server lookup failed (DNS) | ![](05-dc1-dns-and-time/02-stripchart-dns-error.png) |
| DNS failure for internet names | ![](05-dc1-dns-and-time/03-resolve-dnsname-failure.png) |
| Internet access confirmed after DNS forwarder | ![](05-dc1-dns-and-time/04-dc1-internet-confirmed.png) |

## 6. Splunk searches

| | |
| --- | --- |
| **Problem:** wrong field case returns 0 results | ![](06-splunk-searches/01-wrong-field-case-zero-results.png) |
| Events counted by EventCode | ![](06-splunk-searches/02-stats-count-by-eventcode.png) |
| Sorted by count (4907 is mostly noise) | ![](06-splunk-searches/03-eventcode-sorted-by-count.png) |
| Successful logons shown in UTC | ![](06-splunk-searches/04-4624-times-in-utc.png) |
| Same logons after setting Eastern time | ![](06-splunk-searches/05-4624-times-in-eastern.png) |
| Recent successful logons | ![](06-splunk-searches/06-4624-recent-logons.png) |
| Grouped by the wrong field | ![](06-splunk-searches/07-stats-grouped-by-wrong-field.png) |
| Logon type baseline | ![](06-splunk-searches/08-logon-type-breakdown.png) |
| Accounts, all logon types | ![](06-splunk-searches/09-accounts-all-logon-types.png) |
| Accounts with network logons | ![](06-splunk-searches/10-accounts-network-logons.png) |

## 7. Investigations

| | |
| --- | --- |
| Failed logon (4625) detail, [CN-001](../case-notes/CN-001-failed-logon-console.md) | ![](07-investigations/01-4625-failed-logon-detail.png) |
| Anonymous logon search, [CN-002](../case-notes/CN-002-anonymous-network-logon.md) | ![](07-investigations/02-anonymous-logon-search.png) |
| Anonymous logon event | ![](07-investigations/03-anonymous-logon-event.png) |
| Source: CLIENT1, 192.168.10.20 | ![](07-investigations/04-anonymous-logon-network-info.png) |
| NTLM V1 (expected for anonymous) | ![](07-investigations/05-anonymous-logon-ntlm.png) |
