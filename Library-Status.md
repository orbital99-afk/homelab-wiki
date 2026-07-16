---
title: Library Status
description: Current overview of The Library documentation project, active work, and priority reconstruction targets.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Library Status

The Library has grown from a collection of notes into a functioning documentation system for the homelab. It now contains both practical runbooks and the kind of historical record that becomes important after the next reboot.

## Current State

The Library now includes:

- infrastructure pages
- a service catalogue
- runbooks
- an operation archive
- a recovered operation inbox
- the canon
- known goblins
- backup and disaster recovery notes

The project is no longer merely accumulating pages. It is also preserving the distinction between what happened, what was attempted, and what remains uncertain.

## Documented Operations

Completed operation pages currently present:

- [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked)
- [Operation The Fan Was Fine, Ubuntu Was Just Vibes](/Operations/Operation-the-fan-was-fine-ubuntu-was-just-vibes)
- [Operation The Router Has Decided Who Deserves Bandwidth](/Operations/Operation-the-router-has-decided-who-deserves-bandwidth)
- [Operation Spinny Rust Prison Break](/Operations/Operation-spinny-rust-prison-break)
- [Operation Build The Library](/Operations/Build-the-library)
- [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right)
- [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report)
- [Operation Creepy Van Network](/Operations/Operation-creepy-van-network)
- [Operation Fusco, Open The Damn Door](/Operations/Operation-fusco-open-the-damn-door)
- [Operation Preventative Existential Crisis](/Operations/Operation-preventative-existential-crisis)
- [Operation Why Is My 1080p Radarr Hoarding 4K Movies](/Operations/Operation-why-is-my-1080p-radarr-hoarding-4k-movies)
- [Operation One Does Not Simply Migrate Plex](/Operations/Operation-one-does-not-simply-migrate-plex)
- [Operation I Swear We Automated This](/Operations/Operation-i-swear-we-automated-this)
- [Operation Copycat Deluge](/Seedbox/Operation-Copycat-Deluge)

## Needs Reconstruction

| Operation | Priority | Evidence Available | Why It Matters | Next Action |
|---|---|---|---|---|
| Operation Why Is My 1080p Radarr Hoarding 4K Movies | High | Title identified; no dedicated page yet | Captures a recurring media-management problem and would help explain a common operational confusion | Draft a page from available notes, observations, and relevant runbook context |
| Operation I Swear We Automated This | High | Title identified; no dedicated page yet | Useful for documenting automation work that was intended to be reliable but became a lesson in overconfidence | Gather the relevant automation notes and turn them into a structured operation record |
| Operation No More Colon Crimes | High | Title identified; no dedicated page yet | Likely covers a naming, config, or service-path issue that deserves formal documentation | Recover the supporting context and write the operation page |
| Operation Reception Desk | High | Title identified; no dedicated page yet | Likely documents an access, identity, or service-visibility issue that would benefit from a clear record | Find the related evidence and draft the page |
| Operation DNS Shenanigans | Medium | Title identified; no dedicated page yet | DNS issues are easy to forget once the immediate problem is gone, which makes them ideal candidates for reconstruction | Collect supporting notes and document the observed behaviour and resolution |
| Operation Environmental Reconnaissance | Medium | Referenced as a follow-on to Operation Is Reese Being Slowly Baked? | Supports seasonal monitoring and future environmental investigations | Expand the existing context into a dedicated page with the follow-on work |
| Operation Bring Root Inside The Machine | Medium | Title identified; no dedicated page yet | Likely covers a systems-access or privilege-management topic worth preserving | Recover the surrounding evidence and create the page |

## Active / Planned Work

- Tailscale VPN on Demand testing
- Retire or archive the old Fusco backup after verifying Reese backups
- Improve power-cut DNS resilience for grafana.reese
- Continue operation archaeology

## Critical Runbooks

- [Plex](/Runbooks/Plex)
- [Arr Stack](/Runbooks/Arr-Stack)
- [Monitoring](/Runbooks/Monitoring)
- [Backups](/Runbooks/Backups)
- [Tailscale](/Runbooks/Tailscale)
- [WikiJS](/Runbooks/WikiJS)
- [Disaster Recovery](/Operations/Disaster-Recovery-Reese-Dies)

## Documentation Rules

- GitHub is the source of truth.
- Wiki.js pulls from GitHub.
- Major operations need both a technical record and a Committee dramatisation.
- Do not store credentials.
- Archive before deleting.
- Unknown details must remain marked unknown.

## Next Recommended Operation

Operation Why Is My 1080p Radarr Hoarding 4K Movies

The Library is now large enough to require documentation about the documentation. This was inevitable.
