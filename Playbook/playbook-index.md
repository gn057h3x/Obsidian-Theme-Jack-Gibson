# Playbook Index

Cross-engagement knowledge base. Updated on `playbook add` and during `wrap up`.

## By Target Type

### Web App (General)
- [[idor-sequential-id-pcap-creds]] — IDOR on sequential numeric IDs to access other users' resources. Network monitoring apps with PCAP downloads are goldmines for cleartext credentials. Always start at ID 0. #idor #pcap #credential-harvesting

### Windows (SMB)
- [[smb-null-session-enumeration]] — SMB null session share enumeration and file extraction. Non-default shares often contain sensitive data. Note signing status for relay potential. #smb #null-session #windows #enumeration

### Linux (Services)
- [[redis-noauth-data-extraction]] — Redis no-auth data extraction + RCE vectors (webshell, SSH key injection, crontab). Port 6379 outside default nmap range — always scan explicitly. #redis #no-auth #data-extraction #rce

### Linux (Privilege Escalation)
- [[linux-capabilities-setuid-privesc]] — `cap_setuid` on interpreted languages (Python, Perl, Ruby, Node) = instant root via `os.setuid(0)`. `getcap -r /` is as essential as checking SUID. #privesc #capabilities #cap_setuid #linux

## By Technique

### Business Logic / IDOR
- [[idor-sequential-id-pcap-creds]] — Sequential ID enumeration on resource endpoints. PCAP/diagnostic apps expose other users' network captures with cleartext creds.

### Enumeration (Infrastructure)
- [[smb-null-session-enumeration]] — SMB null session enumeration: shares, users, groups, password policy. Check signing for relay.
- [[redis-noauth-data-extraction]] — Redis no-auth: `INFO`, `KEYS *`, `GET`. RCE via `CONFIG SET` (webshell, SSH, cron).

### Privilege Escalation (Linux)
- [[linux-capabilities-setuid-privesc]] — `cap_setuid` on Python/Perl/Ruby/Node = instant root. Always run `getcap -r /`.

## Recon Patterns

- **Redis port 6379** — outside nmap default top 1000. Always `-p 6379` or `-p-`. (See [[redis-noauth-data-extraction]])
- **SMB signing** — `signing enabled but not required` = relay-capable. Note during nmap, exploit later. (See [[smb-null-session-enumeration]])
