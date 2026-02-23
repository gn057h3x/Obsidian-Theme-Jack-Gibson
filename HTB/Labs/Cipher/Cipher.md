---
title: Cipher
platform: HTB
difficulty: Very Easy
os: Linux
ip: 10.10.10.53
status: Completed
engagement_type: lab
tier: 4
date_started: 2026-01-11
date_completed: 2026-01-11
tags:
  - htb
  - very-easy
  - linux
  - database
  - no-auth
---

# Cipher

**Playbook:** [[exposed-database-service-extraction]]

**Hack The Box** · Very Easy · Linux

`Exposed Database` · `No Authentication` · `Data Extraction`

---

## Overview

Cipher is a Very Easy Linux machine with an exposed database service requiring no authentication. Direct access to the database reveals stored credentials and sensitive data, leading to system access and privilege escalation via a misconfigured binary.

---

## Recon

```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu
3306/tcp open  mysql   MySQL 8.0.32
```

Two services: SSH and a MySQL database with no authentication required.

---

## Exploitation (User Flag)

The database accepts connections without credentials. Enumerating the tables reveals user accounts with hashed passwords. One hash is easily cracked, providing SSH access.

---

## Privilege Escalation (Root Flag)

A SUID binary on the system has a known vulnerability allowing privilege escalation to root.

---

## Flags

| Flag | Hash | Method |
|------|------|--------|
| User | `[REDACTED]` | Unauthenticated database → credential extraction → SSH |
| Root | `[REDACTED]` | SUID binary exploitation → root |

## Findings Summary

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| CPH-001 | Database accessible without authentication | Critical | Verified |
| CPH-002 | Weak password hashes in user table | High | Verified |
| CPH-003 | Vulnerable SUID binary allows root escalation | Critical | Verified |

## Attack Chain

```
Port 3306 (MySQL — No Auth)
  → Database enumeration → user credentials
  → Hash cracking → SSH as user → user flag
  → SUID binary exploit → root → root flag
```

## Takeaways

- Database services exposed without authentication are a critical finding. Always check for no-auth access.
- SUID binaries should be part of every Linux privilege escalation checklist.
