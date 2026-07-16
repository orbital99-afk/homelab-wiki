---
title: Operation Fusco, Open The Damn Door
description: Configure reliable SMB mounts from Fusco to Reese for media, backups, and homelab services.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Fusco, Open The Damn Door

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

> **Mount safety warning:** Before deleting or moving files, confirm the Fusco share is actually mounted. Empty local mount points are accomplished liars.

## Status

Completed

## Mission Brief

Ensure Reese could reliably access media and storage shares hosted on Fusco without manual remounting, mysterious empty folders, or services wandering through nonexistent directories.

## Systems Involved

- Reese
- Fusco
- Synology DSM
- SMB / CIFS
- Ubuntu
- `/etc/fstab`
- Plex
- Sonarr
- Radarr1080
- Radarr4K
- Docker bind mounts
- Backup scripts

## The Problem

- Media and storage lived on Fusco.
- Reese needed those shares mounted locally.
- If mounts failed, containers could see empty directories or stale paths.
- Plex and the Arr stack could appear broken even though the applications themselves were healthy.
- Boot timing and network availability could affect mount reliability.
- Permissions and credentials needed to work consistently.

## Investigation

- Confirmed Fusco was reachable over the network.
- Verified that the SMB shares existed and were accessible.
- Checked local mount points on Reese.
- Reviewed mount configuration and credentials.
- Checked ownership and permissions.
- Confirmed Docker containers were using the intended mounted paths.
- Distinguished between:
  - A share not being mounted.
  - A share being mounted but inaccessible.
  - A container bind mount pointing at the wrong local path.

### Safe Diagnostic Commands

These commands reveal mount state without embedding share names, credentials, addresses, or local paths in this page:

```bash
mount | grep -i cifs
findmnt -t cifs
df -h
ls -la <mount-point>
sudo mount -a
systemctl status remote-fs.target
journalctl -b | grep -i cifs
```

## Actions Taken

1. Created or confirmed the required local mount points.
2. Configured SMB/CIFS mounts in `/etc/fstab`.
3. Used a credentials file rather than placing passwords directly in `fstab`.
4. Applied appropriate file and directory ownership options.
5. Added network-aware mount options where appropriate.
6. Verified the mounts after reboot.
7. Confirmed Plex and the Arr stack could see the expected media folders.
8. Documented the danger of empty mount directories: applications may write locally when Fusco is unavailable.

## Outcome

- Reese gained reliable access to Fusco's storage shares.
- Plex and the Arr stack could use consistent local paths.
- Mount checks became part of troubleshooting and maintenance.
- The homelab stopped treating an unavailable share as evidence that every container had died simultaneously.

## Validation

- `mount` or `findmnt` showed active CIFS mounts.
- Expected folders and files were visible from Reese.
- Plex library content remained accessible.
- Sonarr and Radarr could import and manage files.
- Mounts returned after reboot.
- Containers saw the same paths expected by their configurations.

## Casualties

- Several minutes spent staring accusingly at perfectly healthy Docker containers.
- One or more failed `cd..` attempts.
- Trust in empty folders.

## Lessons for Future Daniel

- Check mounts before restarting applications.
- An empty directory does not prove the remote share is mounted.
- Validate both the host path and the container path.
- Never put SMB credentials directly into public documentation.
- Use `sudo mount -a` to test `fstab` changes before rebooting.
- A typo in `fstab` can turn startup into performance art.
- If Fusco is unavailable, avoid letting media applications write into the bare local mount point.

## Best Quote

> “Fusco, open the damn door.”

## Related Documentation

- [Network Map](/Infrastructure/Network-Map)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Plex Runbook](/Runbooks/Plex)
- [Arr Stack Runbook](/Runbooks/Arr-Stack)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Canon](/Canon)
