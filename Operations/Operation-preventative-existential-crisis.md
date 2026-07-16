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

## Objective

Create a repeatable weekly maintenance process that checks the health of Reese and the wider homelab before something breaks at an inconvenient time.

> **Recurrence note:** The operation is recurring because entropy is also recurring.

## Background

The homelab had reached the point where updates, image changes, disk usage, backup health, and stopped containers were spread across too many tools and too many habits. Maintenance had become reactive and improvisational. The Committee therefore authorised a weekly review to bring the work back into a predictable shape before a minor issue transformed into an avoidable incident.

The operation was not intended to eliminate every problem. Its purpose was to make the inevitable problems easier to spot and less likely to arrive as a surprise during the wrong hour of the week.

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

## Phase 1: Establish the Weekly Review

The first phase was to turn maintenance into a checklist rather than a vague promise made in a terminal session.

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

## Phase 2: Operationalise the Routine

Once the review process was defined, it was converted into regular practice.

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

## Notable Findings

- Weekly maintenance was not glamorous, but it was remarkably effective at preventing the sort of surprise failures that make ordinary Tuesday feel like an emergency.
- Diun and ntfy provided a useful notification path, especially once the delivery chain had been tested end to end.
- Backups could take 2–3 hours, which encouraged a more practical question: how do we confirm backup health without waiting an entire afternoon for the whole thing to complete?
- The phrase “No updates needed” was repeatedly encountered and must not be treated as a challenge.
- The Committee confirmed that maintenance is not a one-time problem. It is an ongoing condition.

## Outcome

- Weekly maintenance became a repeatable operation rather than an improvised terminal wander.
- Diun and ntfy provided update notifications.
- Bear, backups, disks, and containers became part of one regular review.
- Future maintenance work gained a consistent starting point.

## Mission Status

COMPLETED — RECURRING

## Validation

- Ubuntu checks completed.
- Docker container state was reviewed.
- No unexpected stopped containers remained.
- Bear reported healthy.
- Backup status was visible.
- An ntfy notification reached the phone.
- Plex remained operational.

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

## Lessons Learned

- Maintenance should be regular, boring, and documented.
- Check before updating.
- Verify backups separately from simply trusting a success message.
- A notification system is only useful if tested end to end.
- Container image updates do not always require immediate action.
- A maintenance window will inevitably generate side quests.
- “No updates needed” is a valid result, not a challenge.
- Entropy is recurring. The schedule should be too.

## Official Findings

The Committee found that a repeatable weekly maintenance process had been established for Reese and the wider homelab. The review covers Ubuntu, Docker, storage, Bear, backups, notifications, and core service health, and it now functions as a structured preventative operation rather than an improvised response to whatever the week has already broken.

## Committee Findings

### Root

> “The checklist exists. The system is now capable of being boring on purpose.”

### Finch

> “That was the objective.”

### Shaw

> “I am pleased to report that the containers were checked before they became interesting.”

### Carter

> “The monitoring data remained visible. The maintenance process finally had a shape.”

### Bear

> “I was online. I was charged. I was not asked to do anything dramatic.”

### Finance Department

> “This is still an expensive way to avoid a surprise outage, but the paperwork is at least consistent.”

## Final Verdict

The homelab was found:

- Not cured of entropy
- Not free from side quests
- Not immune to update noise
- Merely better prepared for the weekly ritual of discovering that something was slightly off

## Follow-On Operations

- Continue the recurring weekly maintenance routine.
- Continue refining backup verification and notification delivery as part of the regular review.

## Series Status

This operation was renewed for another season after investigators confirmed that maintenance is recurring, side quests are recurring, and the Committee has no intention of letting the calendar become a surprise.

## Casualties

- One broken or suspicious Diun notifier.
- Several uses of the word “check”.
- The idea that maintenance could ever be completed without discovering another project.
- At least one existential crisis prevented, though not eliminated.

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
