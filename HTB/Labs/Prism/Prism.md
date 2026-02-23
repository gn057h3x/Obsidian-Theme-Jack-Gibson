---
title: Prism
platform: HTB
difficulty: Easy
os: Linux
ip: 10.10.10.54
status: Completed
engagement_type: lab
tier: 4
date_started: 2026-01-12
date_completed: 2026-01-12
tags:
  - htb
  - easy
  - linux
  - web
  - injection
  - suid
---

# Prism

**Playbook:** [[suid-binary-privilege-escalation]]

**Hack The Box** · Easy · Linux

`Web Application` · `Input Validation Bypass` · `SUID Binary Exploitation`

---

## Overview

Prism is an Easy Linux machine running a custom web application with an input validation flaw. Exploiting the flaw provides a foothold on the system. A misconfigured SUID binary provides the privilege escalation path to root.

---

## Recon

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.0p1 Ubuntu
80/tcp open  http    nginx 1.22.1
```

Two services: SSH and a web application behind nginx.

---

## Exploitation (User Flag)

The web application has a user input field vulnerable to injection. Crafting the right payload achieves command execution on the server as the web application user.

---

## Privilege Escalation (Root Flag)

Enumeration reveals a SUID binary with a known exploitation technique. Running the appropriate command sequence grants a root shell.

---

## Flags

| Flag | Hash | Method |
|------|------|--------|
| User | `[REDACTED]` | Input validation bypass → command execution |
| Root | `[REDACTED]` | SUID binary exploitation → root shell |

## Findings Summary

| ID | Title | Severity | Status |
|----|-------|----------|--------|
| PRM-001 | Input validation flaw allows command execution | Critical | Verified |
| PRM-002 | SUID binary allows privilege escalation to root | Critical | Verified |

## Attack Chain

```
Port 80 (nginx — Web App)
  → Input validation bypass → command execution → user flag
  → SUID binary enumeration → known exploit → root flag
```

## Key Technical Details

### Input Validation Bypass (PRM-001)
- **Endpoint:** User input field on the web application
- **Vulnerability:** Insufficient input sanitization allows injection
- **Impact:** Remote code execution as the application user

### SUID Binary Escalation (PRM-002)
- **Detection:** `find / -perm -4000 2>/dev/null`
- **Impact:** Privilege escalation from user to root

## Takeaways

- Always test user input fields for injection vulnerabilities — they remain the most common web application flaw.
- SUID binary enumeration is a standard step in Linux privilege escalation. Check GTFOBins for known exploitation paths.

## Session Log

- 2026-01-12 — Nmap scan: 2 ports open (22/ssh, 80/http)
- 2026-01-12 — Web application identified, input fields tested
- 2026-01-12 — Injection payload achieved command execution — user flag captured
- 2026-01-12 — SUID enumeration found exploitable binary — root flag captured
- 2026-01-12 — Machine complete.

## References

- [GTFOBins — SUID](https://gtfobins.github.io/)
- [OWASP — Injection](https://owasp.org/www-community/Injection_Flaws)
