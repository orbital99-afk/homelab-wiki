---
title: Plex Runbook
description: Health checks, restart steps, and recovery notes for Plex on Reese.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Plex Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

Plex is the theatre. It serves media from Fusco using the library paths mounted on Reese.

## Where It Lives

- Host: Reese, the primary Ubuntu and Docker host.
- Application configuration generally lives beneath `/opt/docker`.
- Media and Plex data are supplied through mounts from Fusco.
- Related services include Tautulli, Kometa, the Arr stack, and Seerr.

## Quick Health Check

```bash
docker ps
docker logs --tail=100 <plex-container>
df -h
mount | grep -i fusco
```

Also check the Plex UI, play a known item, and confirm its library path points to the expected Fusco mount. If the container is healthy but every library is empty, suspect the Mount Goblin before Plex.

## Restart Procedure

1. Check active streams in Plex or Tautulli and avoid interrupting users where possible.
2. Inspect logs and confirm Fusco mounts are present.
3. Restart only the Plex container:

   ```bash
   docker restart <plex-container>
   ```

4. Watch startup logs and test playback.
5. If managed with Compose, first change into the correct Plex compose directory, then use `docker compose ps` and `docker compose restart <service>`.

## Common Goblins

- **Mount Goblin:** Empty libraries, unavailable media, or old paths after boot.
- **Permission Goblin:** Plex can see files but cannot read or update them.
- **Update Goblin:** New image behaviour, database migrations, or an unhealthy container.
- **Resource pressure:** Slow browsing or transcoding while Reese is short on CPU, memory, or disk space.

## Do Not Casually Delete

Do not delete Plex appdata, its database, metadata, preferences, or Fusco library content. Preserve permissions and paths when restoring. A fresh container with no database is not a repair; it is a new Plex server wearing Reese's name badge.

## Related Pages

- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Monitoring](/Infrastructure/Monitoring)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Known Goblins](/Case-files/Known-Goblins)
