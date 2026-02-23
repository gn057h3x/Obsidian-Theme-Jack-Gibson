---
title: Weak Share Permissions Enumeration
category: techniques
tags: [smb, shares, permissions, windows, enumeration]
source_engagement: HTB-Mirror
date_added: 2026-01-11
---

# Weak Share Permissions Enumeration

**Source:** [[Mirror]] (Very Easy/Windows)

## Technique

Network shares (SMB, NFS) with overly permissive access controls allow unauthenticated or low-privilege users to enumerate and download sensitive files. Guest-level access, null sessions, or anonymous mounts are common misconfigurations.

## When To Use

- Port 445 (SMB) or port 2049 (NFS) open on target
- Windows domain environments with file servers
- Any network service offering file-level access

## Approach

1. Enumerate shares and check for guest/anonymous access
2. List all accessible directories and files recursively
3. Download everything — analyze for credentials, configs, scripts, PII
4. Check file permissions for write access (useful for payload delivery)
5. Note signing and encryption status for potential relay attacks

## Key Signals

> Port 445 open + guest access permitted → full share enumeration.

> Signing enabled but not required → relay attack potential.

## Linked Entries

- Leads to: credential harvesting, lateral movement, data exfiltration
- Combines with: credential reuse, relay attacks
