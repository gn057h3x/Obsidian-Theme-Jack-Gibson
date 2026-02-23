---
title: Relay
platform: HTB
difficulty: Very Easy
os: Linux
ip: 10.10.10.51
status: Completed
engagement_type: lab
tier: 4
date_started: 2026-01-10
date_completed: 2026-01-10
tags:
  - htb
  - very-easy
  - linux
  - anonymous-access
  - ftp
---

# Relay

**Hack The Box** · Very Easy · Linux

`Anonymous Access` · `File Transfer` · `Information Disclosure`

---

## Overview

Relay is a Very Easy Linux machine with an anonymous-access file transfer service. Sensitive files accessible without authentication lead to user credentials and initial access. A misconfigured scheduled task provides the path to root.

---

## Recon

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.5
22/tcp open  ssh     OpenSSH 9.0p1 Ubuntu
```

Two services: an FTP server allowing anonymous access and SSH.

---

## Exploitation (User Flag)

Anonymous access to the file transfer service exposes configuration files containing cleartext credentials. These credentials are reused on SSH for initial access.

---

## Privilege Escalation (Root Flag)

A scheduled task running as root processes files from a user-writable directory. Placing a crafted file in that directory achieves code execution as root.

---

## Flags

| Flag | Hash | Method |
|------|------|--------|
| User | `[REDACTED]` | Anonymous file access → credential extraction → SSH |
| Root | `[REDACTED]` | Writable cron directory → root execution |

## Findings Summary

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| RLY-001 | Anonymous access exposes sensitive files | High | Verified |
| RLY-002 | Credential reuse across services | High | Verified |
| RLY-003 | Writable cron directory allows privilege escalation | Critical | Verified |

## Attack Chain

```
Port 21 (FTP — Anonymous)
  → Sensitive config files → cleartext credentials
  → Password reuse → SSH as user → user flag
  → Writable cron directory → root execution → root flag
```

## Takeaways

- Anonymous access on file services is a common quick win. Always check for it.
- Credential reuse between services is extremely common — always test captured creds across all open ports.
