---
title: Operation Preventative Existential Crisis
description: Establish the recurring weekly maintenance routine for Reese and the wider homelab.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Preventative Existential Crisis

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Status

Completed and recurring

## Mission Brief

Create a repeatable weekly maintenance process that checks the health of Reese and the wider homelab before something breaks at an inconvenient time.

> **Recurrence note:** The operation is recurring because entropy is also recurring.

## Systems Involved

- Reese
- Ubuntu
- Docker
- Portainer / Shaw
- Diun
- Bear / NUT
- Fusco
- Backups
- ntfy
- HealthMonitor
- Plex
- Arr stack
- Monitoring stack

## The Problem

- Updates, image changes, disk usage, backup health, and stopped containers were spread across multiple tools.
- Maintenance was reactive rather than scheduled.
- Daniel wanted a weekly process for checking Ubuntu, containers, storage, UPS status, and backups.
- Diun notifications were not initially working as expected.
- Backup runs could take 2–3 hours, creating interest in a shorter verification check.

## Investigation

- Checked Ubuntu update availability.
- Reviewed running and stopped Docker containers.
- Compared the running container count against expected services.
- Checked disk usage on Reese and Fusco.
- Verified Bear status and battery level.
- Reviewed the latest backup status.
- Checked Diun image-update reporting.
- Investigated ntfy installation and notification delivery.
- Confirmed Plex and core media services remained healthy.
- Considered an abridged backup test rather than waiting for a full backup run.

## Actions Taken

1. Created a weekly maintenance checklist.
2. Applied Ubuntu updates where appropriate.
3. Verified Docker containers were running.
4. Checked for stopped containers.
5. Reviewed Docker image-update notifications through Diun.
6. Checked Reese SSD and Fusco storage usage.
7. Verified Bear was online and charged.
8. Reviewed the latest backup result.
9. Fixed or verified Diun notification delivery.
10. Installed or confirmed ntfy on Reese.
11. Tested ntfy notifications successfully.
12. Added phone notifications.
13. Discussed a shorter backup-validation run to confirm backup health without performing the full 2–3 hour job.

### Example Maintenance Summary

| Check | Expected Summary |
|---|---|
| Ubuntu | Updates available or current |
| Docker | Running containers checked |
| Stopped containers | Zero expected |
| Reese SSD usage | Low |
| Fusco media share | Monitored |
| Bear | `OL` / 100% |
| Backups | Latest run reviewed |
| Notifications | ntfy test successful |

## Outcome

- Weekly maintenance became a repeatable operation rather than an improvised terminal wander.
- Diun and ntfy provided update notifications.
- Bear, backups, disks, and containers became part of one regular review.
- Future maintenance work gained a consistent starting point.

## Validation

- Ubuntu checks completed.
- Docker container state was reviewed.
- No unexpected stopped containers remained.
- Bear reported healthy.
- Backup status was visible.
- An ntfy notification reached the phone.
- Plex remained operational.

## Casualties

- One broken or suspicious Diun notifier.
- Several uses of the word “check”.
- The idea that maintenance could ever be completed without discovering another project.
- At least one existential crisis prevented, though not eliminated.

## Lessons for Future Daniel

- Maintenance should be regular, boring, and documented.
- Check before updating.
- Verify backups separately from simply trusting a success message.
- A notification system is only useful if tested end to end.
- Container image updates do not always require immediate action.
- A maintenance window will inevitably generate side quests.
- “No updates needed” is a valid result, not a challenge.

## Best Quote

> “So no images need updating?”

## Related Documentation

- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Backups Runbook](/Runbooks/Backups)
- [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report)
- [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right)
