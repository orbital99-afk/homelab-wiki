---
title: The Library Wiki.js Runbook
description: Operational checks and recovery guidance for The Library and its database.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# The Library / Wiki.js Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

The Library is the Wiki.js documentation system and institutional memory for the homelab. GitHub remains the source of truth for this Markdown repository.

## Where It Lives

- Host: Reese.
- Wiki.js and PostgreSQL run in Docker.
- Docker configuration and persistent data generally live beneath `/opt/docker`.
- The Markdown export is maintained in GitHub.

## Quick Health Check

```bash
docker ps
docker logs --tail=100 <wikijs-container>
docker logs --tail=100 <postgres-container>
df -h
```

Open The Library and load several pages. Confirm edits or synchronisation behave as expected, and check both the application and database rather than blaming Markdown for a PostgreSQL problem.

## Restart Procedure

1. Inspect Wiki.js and PostgreSQL logs.
2. Confirm disk space and the database container state.
3. If using Compose, change into the correct compose directory first.
4. Use `docker compose ps`, then restart the affected service. Restart PostgreSQL only when evidence points to it, and allow it to become ready before restarting Wiki.js.
5. Confirm pages load and Git synchronisation remains healthy.

## Common Goblins

- **Database goblin:** Wiki.js is running but cannot connect to PostgreSQL.
- **Permission Goblin:** Export or repository files cannot be read or written.
- **DNS Goblin:** Git remote or internal service names fail to resolve.
- **Update Goblin:** Application or database version changes introduce migration issues.
- **Sync confusion:** Wiki.js content and the GitHub source of truth disagree.

## Do Not Casually Delete

Do not delete the PostgreSQL data, Wiki.js configuration, secrets, or Git history. Before replacing persistent data, confirm the nightly backup contents and the current GitHub state. Documentation recovery without its operational history is institutional amnesia with nicer typography.

## Related Pages

- [Canon](/Canon)
- [Backups Runbook](/Runbooks/Backups)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
