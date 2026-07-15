---
title: Disaster Recovery - Reese Dies
description: Practical recovery sequence for rebuilding the primary application host after hardware failure.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Disaster Recovery: Reese Dies

If Reese dies, pause before converting the garage cupboard into a crime scene. Preserve the failed machine and storage until the recovery is complete.

## 1. Confirm the Backup

- Identify the latest completed `/opt/docker` backup in OneDrive.
- Inspect it for compose files, environment files, databases, and application configs.
- Record the backup timestamp and any known gap.
- Do not delete or overwrite older copies during recovery.

## 2. Prepare Replacement Hardware

Use a replacement Mac mini, mini PC, or SFF PC with enough storage, memory, network connectivity, and architecture compatibility for the workload.

1. Install a supported Ubuntu Server release.
2. Apply system updates and configure SSH.
3. Install Docker Engine and Docker Compose.
4. Configure Elias (Tailscale) for remote access.
5. Recreate the expected directory layout, including `/opt/docker`.

## 3. Restore Application Data

Restore the backed-up appdata, compose files, databases, and configs into `/opt/docker`. Protect ownership, permissions, environment files, and secrets. Review host-specific paths before starting containers.

## 4. Recreate Fusco Mounts

- Recreate the media and application-data mounts from Fusco.
- Confirm expected mount points such as `/mnt/fusco/media` and `/mnt/fusco/plexdata`.
- Test read/write permissions where appropriate.
- Ensure mounts persist across reboot before starting the media stack.

## 5. Bring Up Core Services

Start services in a controlled order:

1. Shaw (Portainer)
2. Plex
3. Arr stack: Prowlarr, Sonarr, Radarr1080, Radarr4K, and Seerr
4. Monitoring: Prometheus, Grafana, exporters, Carter (Uptime Kuma), and ntfy
5. The Library (Wiki.js and its database)

Bring up supporting services after the core is stable. Starting everything at once produces an exciting wall of logs and very little evidence.

## 6. Validate

- **Plex:** confirm libraries resolve to the correct Fusco paths and test playback.
- **Seerr:** submit a test request and verify it reaches the correct Arr application.
- **Grafana:** confirm dashboards receive current Prometheus data.
- **Carter:** confirm Uptime Kuma checks are active and correctly report service state.
- **Bear:** confirm NUT and UPS telemetry are visible.
- **The Library:** confirm pages load and the database is persistent.
- Reboot once and verify mounts, Docker stacks, remote access, and monitoring recover automatically.

## 7. Close the Incident

Document the failed component, replacement hardware, backup used, data loss if any, configuration changes, and validation results. Keep the old Reese and all recovery media untouched until the rebuilt host has completed backups and survived a sensible observation period.

Then, and only then, may the committee declare Reese “mostly alive.”
