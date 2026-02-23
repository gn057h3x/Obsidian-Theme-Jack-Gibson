---
title: Beacon
platform: HTB
difficulty: Very Easy
os: Linux
ip: 10.10.10.50
status: Completed
engagement_type: lab
tier: 4
date_started: 2026-01-10
date_completed: 2026-01-10
tags:
  - htb
  - very-easy
  - linux
  - default-creds
  - web
---

# Beacon

**Playbook:** [[default-credentials-management-interfaces]]

**Hack The Box** · Very Easy · Linux

`Default Credentials` · `Web Administration Panel` · `Service Misconfiguration`

---

## Overview

Beacon is a Very Easy Linux machine hosting a web administration panel with default credentials. Access to the admin panel reveals system configuration options that lead to command execution and full system compromise.

---

## Recon

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu
80/tcp open  http    Apache httpd 2.4.52
```

Two services: SSH and a web application on Apache. The web app is the entry point.

---

## Exploitation (User Flag)

The web application hosts a management dashboard. Default credentials grant admin access, exposing system utilities that allow command execution. User flag obtained from the web user's home directory.

---

## Privilege Escalation (Root Flag)

A misconfigured service running as root accepts commands from the admin panel. Leveraging this service provides root-level access and the root flag.

---

## Flags

| Flag | Hash | Method |
|------|------|--------|
| User | `[REDACTED]` | Default credentials → admin panel → command execution |
| Root | `[REDACTED]` | Misconfigured service → root access |

## Findings Summary

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| BCN-001 | Default credentials on management panel | High | Verified |
| BCN-002 | Command execution via admin utilities | Critical | Verified |

## Attack Chain

```
Port 80 (Apache — Admin Panel)
  → Default credentials → admin access
  → System utilities → command execution → user flag
  → Misconfigured root service → root flag
```

## Takeaways

- Always test default credentials on management interfaces before attempting complex attacks.
- Admin panels often expose system-level functionality that developers assume is protected by authentication alone.
