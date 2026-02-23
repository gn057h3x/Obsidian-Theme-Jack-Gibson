---
title: SUID Binary Privilege Escalation
category: techniques
tags: [privesc, suid, linux, binary-exploitation]
source_engagement: HTB-Prism
date_added: 2026-01-12
---

# SUID Binary Privilege Escalation

**Source:** [[Prism]] (Easy/Linux)

## Technique

SUID (Set User ID) binaries execute with the permissions of the file owner rather than the calling user. When root-owned binaries with SUID are exploitable (via GTFOBins techniques, custom vulnerabilities, or PATH manipulation), they provide a direct privilege escalation path to root.

## When To Use

- Standard Linux privilege escalation enumeration
- After obtaining any user-level shell on a Linux system
- When other privesc vectors (sudo, cron, capabilities) don't yield results

## Approach

1. Find SUID binaries: `find / -perm -4000 2>/dev/null`
2. Cross-reference with GTFOBins for known exploitation techniques
3. Check for custom/unusual SUID binaries (not standard system utilities)
4. Test PATH manipulation if the binary calls other commands without absolute paths
5. Check for writable libraries loaded by the binary

## Key Signals

> Custom SUID binary (not a standard utility) → high exploitation probability.

> SUID binary calling other commands without absolute paths → PATH hijack.

## Linked Entries

- Combines with: writable PATH directories, library injection
- Related: Linux capabilities (`getcap -r /`), sudo misconfigurations
