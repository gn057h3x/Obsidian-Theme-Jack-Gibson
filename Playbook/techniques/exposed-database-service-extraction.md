---
title: Exposed Database Service Extraction
category: techniques
tags: [database, no-auth, mysql, redis, data-extraction]
source_engagement: HTB-Cipher
date_added: 2026-01-11
---

# Exposed Database Service Extraction

**Source:** [[Cipher]] (Very Easy/Linux)

## Technique

Database services exposed to the network without authentication (or with default credentials) allow direct data extraction. Common targets include MySQL, PostgreSQL, Redis, MongoDB, and Elasticsearch.

## When To Use

- Database ports open during scanning (3306, 5432, 6379, 27017, 9200)
- Known database service identified in banner grab
- Application configs referencing database connection strings

## Approach

1. Attempt connection without credentials or with common defaults
2. Enumerate databases, tables, and schemas
3. Extract user tables — look for credentials (plaintext or hashed)
4. Check for stored procedures, triggers, or functions that indicate system access
5. Test for file read/write capabilities (INTO OUTFILE, LOAD_FILE, etc.)

## Key Signals

> Database port open + no auth required → direct data access.

> User table with hashed passwords → offline cracking opportunity.

## Linked Entries

- Leads to: credential harvesting, file system access, RCE via database features
- Combines with: password cracking, credential reuse
