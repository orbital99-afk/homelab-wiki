---
title: Known Goblins
description: A practical field guide to recurring homelab problems and their usual suspects.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Known Goblins

Some incidents are unique. Others wear a fake moustache and return every six weeks. Check this field guide before declaring a new and exciting catastrophe.

## The Permission Goblin

**Symptoms:** A backup job or Docker application cannot read or write files. Logs contain permission-denied errors, or files appear but cannot be changed.

**Usual suspects:** Ownership, bind-mount permissions, Synology permissions, and mismatched container UID/GID values.

**First checks:** Compare ownership and permissions on the host and inside the container. Confirm the mounted path is the expected path before changing permissions recursively.

## The DNS Goblin

**Symptoms:** Friendly names fail, direct IP access works, and the browser sulks as though this were a personal betrayal.

**Usual suspects:** Router DNS, Tailscale MagicDNS, and AdGuard, Caddy, or reverse-proxy configuration.

**First checks:** Test name resolution from the affected client, confirm which DNS server answered, and verify the proxy target independently.

## The YAML Goblin

**Symptoms:** A service refuses to start after “one tiny edit.” Compose or application logs complain about parsing, structure, or fields that definitely existed five minutes ago.

**Usual suspects:** Indentation, tabs, a missing colon, and copy/paste betrayal.

**First checks:** Validate the configuration, inspect the exact changed lines, and compare indentation with neighbouring entries. HR has opened a file.

## The Mount Goblin

**Symptoms:** Plex or the Arr stack sees empty folders, missing libraries, or paths from a previous life.

**Usual suspects:** The Fusco SMB mount, `/etc/fstab`, mount credentials, or the network not being ready at boot.

**First checks:** Confirm the mount exists, contains expected data, and has correct permissions. Do not let an application populate an empty local mount point by accident.

## The Thermal Goblin

**Symptoms:** Reese gets spicy, the fan sounds suspicious, or the cupboard temperature delta begins auditioning for a disaster film.

**Usual suspects:** Restricted airflow, `macfanctld`, cupboard temperature, dust, and garage heat.

**First checks:** Review temperature trends and fan RPM, inspect airflow, and confirm the fan-control service is healthy before adding more workloads.

## The Update Goblin

**Symptoms:** “It worked yesterday.” A container restarts, behaves differently, or develops a new opinion about its configuration.

**Usual suspects:** Docker image updates, breaking changes, stale containers, and unpinned versions.

**First checks:** Review Diun notices and release notes, identify the running image version, inspect recent container recreation, and confirm a rollback path before experimenting.

---

When a goblin develops a genuinely new trick, update this page or open a case file. Recurring incidents are only folklore when nobody writes down the fix.
