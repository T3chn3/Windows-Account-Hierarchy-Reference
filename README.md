# Windows Account Hierarchy — Threat Hunter Reference

A single-file interactive HTML reference covering the full Windows account privilege stack, from `NT AUTHORITY\SYSTEM` down to `Guest`, including Active Directory management accounts.

## Purpose

Built for threat hunters and blue teamers who need a fast, authoritative lookup during investigations, hunt planning, or detection engineering. Every account includes hunt signals and a ready-to-use MDE KQL query.

## Coverage

| Tier | Accounts |
|---|---|
| Kernel / OS | NT AUTHORITY\SYSTEM, NETWORK SERVICE, LOCAL SERVICE |
| Active Directory | Domain Admins, Enterprise Admins, Schema Admins, Account Operators, Backup Operators, KRBTGT |
| Local Admin | Built-in Administrator (RID-500), LAPS Managed Account |
| Domain User | Standard Domain User, Remote Desktop Users |
| Service & Managed | gMSA/sMSA, Legacy Service Account, NT SERVICE\\\<Name\> virtual accounts |
| Restricted | Built-in local user, DefaultAccount, WDAGUtilityAccount, Guest |

## What Each Entry Contains

- **SID** with field-level breakdown (revision, authority, RID)
- **Key attributes** — logon type, network identity, password behavior, scope
- **Privileges** color-coded by severity (critical / elevated / standard)
- **Hunt signals** — specific behaviors and event IDs to alert on
- **MDE KQL query** — copy-ready for Microsoft Defender for Endpoint
- **MITRE ATT&CK techniques** mapped to each account type

## Usage

Open `windows_account_hierarchy.html` in any modern browser. No server, no dependencies, no internet connection required — everything is self-contained.

Click any account in the left panel to load its full breakdown on the right. KQL blocks have a one-click copy button.

## Notes

- SIDs containing `<domain>` or `<machine>` are placeholders for the domain or machine-specific identifier component, which varies per environment.
- KQL queries target **Microsoft Defender for Endpoint** (`DeviceProcessEvents`, `DeviceFileEvents`) and **Windows Security Event Log** (`SecurityEvent`). Adjust table names for your SIEM as needed.
- KRBTGT password rotation guidance: always rotate twice in succession after any domain-level compromise to invalidate existing Golden Tickets.

## References

- [Microsoft: Well-known SIDs](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers)
- [MITRE ATT&CK Enterprise](https://attack.mitre.org/matrices/enterprise/)
- [CIS Benchmark for Windows Server](https://www.cisecurity.org/cis-benchmarks)
- [DISA STIG for Windows](https://public.cyber.mil/stigs/)
- [Microsoft LAPS documentation](https://learn.microsoft.com/en-us/windows-server/identity/laps/laps-overview)
