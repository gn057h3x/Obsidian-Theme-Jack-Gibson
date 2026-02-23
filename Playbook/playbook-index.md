# Playbook Index

Cross-engagement knowledge base. Updated on `playbook add` and during `wrap up`.

## By Target Type

### Web App (General)
- [[default-credentials-management-interfaces]] — Default credential testing on admin panels, appliance dashboards, and management interfaces. Always test before brute-forcing. #default-creds #web #admin-panel

### Windows (SMB)
- [[weak-share-permissions-enumeration]] — Network share enumeration with guest/anonymous access. Download everything, check for credentials and configs. Note signing status for relay potential. #smb #shares #windows #enumeration

### Linux (Services)
- [[exposed-database-service-extraction]] — Database services (MySQL, Redis, MongoDB) exposed without authentication. Enumerate tables, extract credentials, test for file access and RCE vectors. #database #no-auth #data-extraction

### Linux (Privilege Escalation)
- [[suid-binary-privilege-escalation]] — SUID binary exploitation via GTFOBins, PATH manipulation, or custom vulnerabilities. `find / -perm -4000` is essential in every Linux privesc checklist. #privesc #suid #linux

## By Technique

### Authentication Weaknesses
- [[default-credentials-management-interfaces]] — Default credentials on management panels and appliance interfaces. Check vendor docs and common pairs.

### Enumeration (Infrastructure)
- [[weak-share-permissions-enumeration]] — SMB/NFS share enumeration with weak access controls. Recursive download and credential search.
- [[exposed-database-service-extraction]] — No-auth database access: enumerate schemas, extract users, test file operations.

### Privilege Escalation (Linux)
- [[suid-binary-privilege-escalation]] — SUID binaries with known GTFOBins exploits or PATH manipulation opportunities. Always run `find / -perm -4000`.

## Recon Patterns

- **Login pages on management interfaces** — Always test default credentials before brute-forcing. (See [[default-credentials-management-interfaces]])
- **SMB signing** — `signing enabled but not required` = relay-capable. Note during scanning. (See [[weak-share-permissions-enumeration]])
