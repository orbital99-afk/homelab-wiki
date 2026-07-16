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

## Objective

Ensure Reese could reliably access media and storage shares hosted on Fusco without manual remounting, mysterious empty folders, or services wandering through nonexistent directories.

The objective was not merely to make the share visible. It was to prevent the homelab from mistaking a missing mount for an application failure and then panicking in the wrong direction.

## Background

Media and storage lived on Fusco, but Reese needed those shares mounted locally in a way that containers, Plex, and backup scripts could depend on. When mount failures occurred, the symptoms could be misleading: healthy services appeared broken, empty directories looked like evidence, and the investigation became a chase through the wrong layer of the stack.

The Committee therefore authorised a mount-focused operation to determine whether the problem was storage access, service configuration, or the very convincing lie of an empty local folder.

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

## Phase 1: Confirm the Share and the Fault Domain

The first phase involved proving whether Fusco was reachable and whether the problem was a mount issue or a container-path issue.

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

## Phase 2: Repair the Mount Path

Once the fault domain was clear, the mount configuration itself was corrected and verified.

1. Created or confirmed the required local mount points.
2. Configured SMB/CIFS mounts in `/etc/fstab`.
3. Used a credentials file rather than placing passwords directly in `fstab`.
4. Applied appropriate file and directory ownership options.
5. Added network-aware mount options where appropriate.
6. Verified the mounts after reboot.
7. Confirmed Plex and the Arr stack could see the expected media folders.
8. Documented the danger of empty mount directories: applications may write locally when Fusco is unavailable.

## Notable Findings

- Empty directories were not a reliable sign of a healthy share. They were, in fact, excellent liars.
- Perfectly healthy Docker containers could be blamed for storage issues simply because the mount path they were using was absent or wrong.
- The problem was frequently not the application. It was the path, the mount, or the moment when the share was unavailable and the system quietly wrote to the wrong place.
- The Committee found that mounting a network share is not glamorous, but it is more useful than blaming Plex for the sins of the filesystem.

## Outcome

- Reese gained reliable access to Fusco's storage shares.
- Plex and the Arr stack could use consistent local paths.
- Mount checks became part of troubleshooting and maintenance.
- The homelab stopped treating an unavailable share as evidence that every container had died simultaneously.

## Mission Status

COMPLETED

## Validation

- `mount` or `findmnt` showed active CIFS mounts.
- Expected folders and files were visible from Reese.
- Plex library content remained accessible.
- Sonarr and Radarr could import and manage files.
- Mounts returned after reboot.
- Containers saw the same paths expected by their configurations.

## Lessons Learned

- Check mounts before restarting applications.
- An empty directory does not prove the remote share is mounted.
- Validate both the host path and the container path.
- Never put SMB credentials directly into public documentation.
- Use `sudo mount -a` to test `fstab` changes before rebooting.
- A typo in `fstab` can turn startup into performance art.
- If Fusco is unavailable, avoid letting media applications write into the bare local mount point.
- A mount point may look like a directory. It may also be an elaborate misunderstanding.

## Official Findings

The Committee determined that the storage path issue was resolved through proper SMB/CIFS mount configuration, correct local mount points, and verification of the relevant container and service paths. The result was reliable access to Fusco-backed media and storage resources on Reese.

## Committee Findings

### Root

> “We discovered that the containers were not the problem. The mount point was the problem. This is an important lesson and also a personal insult.”

### Finch

> “So the containers were healthy?”

### Fusco

> “I was available. The door was just not open.”

### Plex

> “I was fine. The folder just wasn’t there.”

### HR

> “This is why we maintain a policy against misleading directories.”

## Final Verdict

Fusco was found:

- Not hostile
- Not empty in the way the local path suggested
- Not responsible for the emotional distress of the containers
- Merely unavailable until mounted properly

## Follow-On Operations

- Continue validating mounts after reboot as part of routine maintenance.
- Continue checking host paths and container bind mounts whenever media services appear inconsistent.

## Series Status

This operation was renewed for another season after investigators discovered that storage mounts are recurring, the path is always suspicious, and the door is never truly open until somebody checks it properly.

## Casualties

- Several minutes spent staring accusingly at perfectly healthy Docker containers.
- One or more failed `cd..` attempts.
- Trust in empty folders.

## Best Quote

> “Fusco, open the damn door.”

## Related Documentation

- [Network Map](/Infrastructure/Network-Map)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Plex Runbook](/Runbooks/Plex)
- [Arr Stack Runbook](/Runbooks/Arr-Stack)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Canon](/Canon)
