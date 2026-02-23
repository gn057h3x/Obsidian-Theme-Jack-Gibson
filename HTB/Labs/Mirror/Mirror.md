---
title: Mirror
platform: HTB
difficulty: Very Easy
os: Windows
ip: 10.10.10.52
status: Completed
engagement_type: lab
tier: 4
date_started: 2026-01-11
date_completed: 2026-01-11
tags:
  - htb
  - very-easy
  - windows
  - smb
  - weak-permissions
---

# Mirror

**Playbook:** [[weak-share-permissions-enumeration]]

**Hack The Box** · Very Easy · Windows

`Network Shares` · `Weak Permissions` · `Information Disclosure`

---

## Overview

Mirror is a Very Easy Windows machine with misconfigured network share permissions. Guest-level access to shares reveals sensitive documents including credentials that provide administrative access.

---

## Recon

```
PORT    STATE SERVICE      VERSION
135/tcp open  msrpc        Microsoft Windows RPC
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Windows Server 2019
```

Standard Windows services with SMB exposed.

---

## Exploitation (User Flag)

Guest-level access to network shares is permitted without credentials. Enumerating the shares reveals documents containing user credentials for remote access.

---

## Privilege Escalation (Root Flag)

Further share enumeration with the obtained credentials reveals administrative credentials stored in a configuration file, granting full system access.

---

## Flags

| Flag | Hash | Method |
|------|------|--------|
| User | `[REDACTED]` | Guest share access → credential extraction → remote login |
| Root | `[REDACTED]` | Config file in restricted share → admin credentials |

## Findings Summary

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| MRR-001 | Guest access to network shares | High | Verified |
| MRR-002 | Credentials stored in plaintext on share | High | Verified |
| MRR-003 | Admin credentials in configuration file | Critical | Verified |

## Attack Chain

```
Port 445 (SMB)
  → Guest access → share enumeration
  → Sensitive documents → user credentials → user flag
  → Restricted share → admin config file → admin access → root flag
```

## Takeaways

- Network shares with weak permissions are one of the most common findings in Windows environments.
- Always enumerate all accessible shares and check file contents for credentials.
