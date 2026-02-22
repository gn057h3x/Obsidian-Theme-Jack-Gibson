# Playbook — Overview & Quick Reference

> **This is the lightweight index.** Peep this at session start, engagement briefing, or anytime you need a fast lookup. It's the table of contents — not the full library. For detailed entries, follow the `[[wikilinks]]` to individual files. For full playbook operations (add, search, review), see `playbook-reference.md`.

---

## What Is The Playbook?

The playbook is a living knowledge base built from **real engagements and labs** — not textbook theory. Every technique, chain, bypass, and failure recorded here was tested against a real target. It grows after every engagement and feeds forward into the next one.

**Structure:**
```
Playbook/
├── pbindex.md              ← YOU ARE HERE (overview, signals, quick ref)
├── playbook-index.md       ← Full categorized index with tags
└── techniques/             ← Proven attack techniques (4 entries)
```

---

## Recon Signals → Techniques

When you see this during enumeration, check the linked playbook entry first.

| Signal | What To Check | Playbook Entry |
|--------|--------------|----------------|
| Port 6379 open | Redis no-auth → data dump, RCE via CONFIG SET | [[redis-noauth-data-extraction]] |
| Port 445 + null session | SMB share enum → sensitive files, user lists | [[smb-null-session-enumeration]] |
| Sequential numeric IDs in URLs | IDOR → access other users' data/files | [[idor-sequential-id-pcap-creds]] |
| `getcap` shows `cap_setuid` | Instant root via interpreted language | [[linux-capabilities-setuid-privesc]] |
| SMB signing not required | Relay attack potential (ntlmrelayx) | [[smb-null-session-enumeration]] |
| FTP/Telnet/HTTP Basic in PCAP | Cleartext credential extraction | [[idor-sequential-id-pcap-creds]] |

---

## Stats

| Category | Count |
|----------|-------|
| Techniques | 4 |
| Chains | 0 |
| Bypasses | 0 |
| Recon Patterns | 2 |
| Failures | 0 |
| **Total Entries** | **4** |

*Last updated: 2026-02-21*

---

## Playbook Sources

| Source | Entries From | Type |
|--------|-------------|------|
| HTB Dancing (Starting Point, Very Easy/Windows) | 1 (SMB null session) | Lab |
| HTB Redeemer (Starting Point, Very Easy/Linux) | 1 (Redis no-auth) | Lab |
| HTB Cap (Easy/Linux) | 2 (IDOR/PCAP, cap_setuid) | Lab |

---

## High-Bounty Patterns

Vulnerability classes that typically pay well on bug bounty platforms. Prioritize these during BB hunting.

| Signal | Vulnerability Class | Why It Pays | Typical Severity |
|--------|-------------------|-------------|-----------------|
| GraphQL endpoint with introspection enabled | Information disclosure + auth bypass | Exposes full API schema, often leads to BOLA/BFLA | Medium–High |
| Sequential/predictable resource IDs | IDOR | Direct data access across accounts, scales to all users | High |
| JWT with weak/no verification | Authentication bypass | Full account takeover, often pre-auth | Critical |
| File upload with insufficient validation | RCE via webshell | Server compromise, highest impact class | Critical |
| Password reset with predictable tokens | Account takeover | Affects all users, no interaction required | High–Critical |
| Race condition on transaction endpoints | Business logic abuse | Financial impact, hard to detect/fix | High |
| SSRF on URL-accepting features | Internal service access | Cloud metadata exposure (AWS keys), internal network pivot | High–Critical |
| OAuth redirect_uri with open redirect | Token theft | Account takeover via social engineering | High |
| Admin panel accessible without auth | Privilege escalation | Full application compromise | Critical |
| API returning more data than UI shows | Excessive data exposure | PII leakage at scale, GDPR implications | Medium–High |

---

## Common Duplicates

Findings commonly already reported on active programs. **Check before submitting** — search disclosed reports and recent submissions first.

| Finding Class | Why It's Commonly Duplicated | Before Submitting |
|--------------|-----------------------------|--------------------|
| Missing rate limits on login | Every hunter tests this first | Check if program explicitly excludes rate limiting issues |
| Self-XSS | Low impact, most programs mark as informative | Only submit if chainable (e.g., self-XSS + CSRF = stored XSS) |
| CSRF on non-state-changing endpoints | No security impact | Only submit CSRF on actions that modify data or state |
| Open redirect (standalone) | Low impact unless chainable | Chain with OAuth token theft or phishing for higher severity |
| Missing security headers (HSTS, CSP, etc.) | Informational, most programs exclude | Check program policy — most explicitly exclude header issues |
| SPF/DKIM/DMARC misconfiguration | Email security, usually out of scope | Check if email domain is in scope and program cares about email |
| Clickjacking on non-sensitive pages | Low impact | Only report on pages with sensitive actions (transfer, settings) |
| CORS misconfiguration (wildcard on non-sensitive API) | Often low impact | Only report if credentials are reflected and sensitive data exposed |
| Subdomain takeover (on non-critical subdomain) | Commonly reported, often already known | Verify the subdomain is actually dangling and hosts sensitive context |
| Verbose error messages / stack traces | Information disclosure, low severity | Only report if errors expose credentials, internal paths, or PII |

---

## How The Playbook Grows

```
 Lab / Engagement
       │
       ▼
   BRIEFING ──→ Search pbindex.md for matching signals
       │         Surface relevant techniques before testing
       │
   TESTING ──→  When technique works: note it for debrief
       │         When technique fails: note it for debrief
       │
  DEBRIEFING ──→ Write playbook entries (technique/chain/failure)
       │         Update pbindex.md signals table
       │         Update playbook-index.md categories
       │         Write walkthrough (labs) or report (clients)
       │
       ▼
   NEXT ENGAGEMENT ──→ pbindex.md surfaces what you learned
```
