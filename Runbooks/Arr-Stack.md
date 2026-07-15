---
title: Arr Stack Runbook
description: Operational checks and safe restart guidance for the media automation stack.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Arr Stack Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

The Arr stack manages media discovery, requests, acquisition, and organisation. Sonarr handles television; Radarr1080 is the sensible movie department; Radarr4K is the show pony division; Prowlarr manages indexers; and Seerr is the request desk with approval and veto power. Kometa and Tautulli support Plex metadata and activity reporting.

TV requests must not be approved blindly without checking season selection. “All seasons” is a storage decision wearing a friendly button.

## Where It Lives

- Host: Reese.
- Docker appdata and compose configuration generally live beneath `/opt/docker`.
- Media paths and storage are mounted from Fusco.
- Services: Sonarr, Radarr1080, Radarr4K, Prowlarr, Jellyseerr/Seerr, Kometa, and Tautulli.

## Quick Health Check

```bash
docker ps
docker logs --tail=100 <container>
df -h
mount | grep -i fusco
```

In each UI, review health warnings, queues, failed imports, root folders, indexer status, and download-client connectivity. In Seerr, verify requests route to the intended Sonarr or Radarr instance with the correct quality profile and season selection.

## Restart Procedure

1. Identify the failing service and inspect its logs and dependencies.
2. Confirm Fusco mounts exist and required upstream services are reachable.
3. Restart only the affected container with `docker restart <container>`.
4. If the stack uses Compose, change into its correct compose directory first:

   ```bash
   docker compose ps
   docker compose restart <service>
   ```

5. Recheck health warnings, integrations, queues, and one representative request or import.

## Common Goblins

- **Mount Goblin:** Empty root folders or imports targeting stale paths.
- **Permission Goblin:** Downloads exist but cannot be imported or renamed.
- **DNS Goblin:** Indexers, download clients, or sibling services cannot resolve one another.
- **Update Goblin:** API compatibility or configuration changes after image updates.
- **Profile confusion:** 1080p work reaches Radarr4K, or Seerr routes requests to the wrong department.

## Do Not Casually Delete

Do not delete databases, appdata, API settings, root-folder mappings, quality profiles, custom formats, indexer definitions, or Seerr request history. Do not “fix” a missing mount by changing every root folder to an empty local directory.

## Related Pages

- [Plex Runbook](/Runbooks/Plex)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Backups Runbook](/Runbooks/Backups)
- [Known Goblins](/Case-files/Known-Goblins)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
