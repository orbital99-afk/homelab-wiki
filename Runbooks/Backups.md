---
title: Backups Runbook
description: Checks, failure handling, and restore safeguards for the nightly Reese backup.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Backups Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

The backup process protects Reese's Docker appdata and configuration. `/opt/docker` is backed up nightly to OneDrive using rclone, and recent Daily HealthMonitor report zips are rotated separately.

## Where It Lives

- Source host: Reese.
- Primary known source: `/opt/docker`.
- Remote destination: OneDrive through the configured rclone remote.
- Fusco may retain historical backup material that must not be deleted casually.

## Quick Health Check

```bash
df -h
systemctl status docker
```

Review the most recent scheduled-job result and logs using the scheduler actually configured on Reese. Confirm the latest backup timestamp and inspect its contents. Verify that compose files, application configs, environment files, and required databases are represented without exposing secrets in notes or screenshots.

## Restart Procedure

Backups are jobs rather than a service to kick reflexively.

1. Read the failed job output and identify whether the source, network, authentication, capacity, or rclone operation failed.
2. Confirm `/opt/docker` is readable and OneDrive connectivity is available.
3. Check the configured schedule and command on Reese.
4. Re-run the established backup job only after understanding whether it could overwrite or delete remote data.
5. Confirm successful completion and inspect the resulting backup.

## Common Goblins

- **Permission Goblin:** The job cannot read Docker appdata or write temporary files.
- **Network or authentication failure:** OneDrive cannot be reached or the configured remote is no longer authorised.
- **Capacity issue:** Local staging or remote storage is full.
- **False success:** The job completes but excludes important files or contains no useful data.
- **Retention enthusiasm:** A cleanup rule removes the only known-good recovery point.

## Do Not Casually Delete

Never delete old backups merely because a newer backup exists. Archive or disable old Fusco/Synology backups first, prove Reese's replacement backup covers `/opt/docker` and key configs, and test a restore before final deletion. Do not alter rclone deletion or synchronisation behaviour without reviewing its consequences.

## Related Pages

- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [The Library Runbook](/Runbooks/WikiJS)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Known Goblins](/Case-files/Known-Goblins)
