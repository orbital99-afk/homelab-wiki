---
title: Backups and Restore
description: Current backup approach, retention safeguards, and restore principles for the homelab.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Backups and Restore

> **Warning:** Do not delete old backups just because a new backup exists. That is how horror movies start.

## Current Approach

Reese backs up `/opt/docker` to OneDrive nightly using rclone. This directory contains the compose and application data needed to reconstruct most services, but a successful command is not the same as a proven restore.

The Daily HealthMonitor report is zipped and rotated so recent reports remain available without collecting forever like digital newspapers in a hallway.

## Fusco and Historical Backups

Fusco previously held backup responsibilities. Any old Synology/Fusco backup may be retired only after confirming that Reese's nightly backup includes all of `/opt/docker` and the key configuration required to rebuild services.

Never delete an old backup immediately. Archive or disable it first, allow the replacement process to complete several successful cycles, and perform a restore test before final removal.

## Restore Philosophy

- Backups are not real until restored.
- Configs matter more than vibes.
- Screenshots are not backups, but they are excellent breadcrumbs.
- Archive before deleting.
- Reese can be replaced; undocumented weirdness cannot.

## Restore Thinking

1. Identify the newest completed backup and inspect its contents.
2. Confirm compose files, environment files, databases, and application configs are present.
3. Restore into a staging location when possible rather than over the live copy.
4. Recreate Fusco mounts and verify paths before starting media services.
5. Start core infrastructure in dependency order, then validate each service.
6. Record the restore date, backup used, gaps found, and corrective work in The Library.

Credentials and secrets may require a separate protected recovery method. Document where they can be recovered without placing the secrets themselves in this export.
