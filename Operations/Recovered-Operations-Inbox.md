---
title: Recovered Operations Inbox
description: Temporary evidence locker for operations recovered from old ChatGPT conversations.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Recovered Operations Inbox

This page temporarily holds operation names, fragments, remembered outcomes, jokes, and uncertain details recovered from old ChatGPT conversations.

> **This is an evidence locker, not final canon. Entries graduate to full operation pages after reconstruction.**

| Operation | Approximate Date | Systems Involved | What Happened | Outcome | Confidence | Full Page Needed? |
|---|---|---|---|---|---|---|
| [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right) | July 2026 validation | Reese; Bear; NUT; Prometheus; Grafana; HealthMonitor; ntfy; UPS exporter | Connected Bear to Reese using NUT and integrated UPS health into homelab monitoring. | Completed and documented; live telemetry was restored after replacing a faulty USB cable, while native runtime remained unavailable. | Confirmed | No |
| [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report) | Unknown | Reese; HealthMonitor; cron; Docker; Bear; backups; notifications | Created the daily homelab health report and repaired cron after it continued calling the obsolete script path. | Completed and documented; reports now run automatically, produce rotating ZIP files, and deliver through email and ntfy. | Confirmed | No |
| [Operation Creepy Van Network](/Operations/Operation-creepy-van-network) | Unknown | Elias / Tailscale; Reese; client devices; MagicDNS | Rolled out secure remote access through Tailscale and added MagicDNS for friendlier device access. | Completed and documented; VPN-on-Demand testing and broader friendly-name integration remain planned. | Confirmed | No |
| [Operation Fusco, Open The Damn Door](/Operations/Operation-fusco-open-the-damn-door) | Unknown | Reese; Fusco; Synology DSM; SMB/CIFS; Plex; Arr stack; backups | Configured reliable SMB mounts from Fusco to Reese and verified host and container storage access. | Completed and documented; mount validation is now part of troubleshooting and maintenance. | Confirmed | No |
| [Operation Preventative Existential Crisis](/Operations/Operation-preventative-existential-crisis) | Unknown; recurring | Reese; Docker; Fusco; Bear; backups; notifications; monitoring | Established the weekly maintenance process for updates, containers, storage, UPS health, backups, notifications, and core services. | Completed, documented, and recurring; the Saturday Maintenance Runbook remains the practical checklist. | Confirmed | No |
| [Operation Why Is My 1080p Radarr Hoarding 4K Movies](/Operations/Operation-why-is-my-1080p-radarr-hoarding-4k-movies) | May 24, 2026 | Seerr / Jellyseerr; Radarr1080; Radarr4K; Plex; Fusco; download client | A Seerr request-specific Ultra-HD override caused a movie request to be added to Radarr1080 with a 4K profile, which then grabbed a 2160p WEB-DL before the file was moved to Radarr4K. | Completed and documented; the 4K file was preserved and imported into the 4K library. | Confirmed | No |
| [Operation One Does Not Simply Migrate Plex](/Operations/Operation-one-does-not-simply-migrate-plex) | Unknown | Reese; Fusco; Plex; Ubuntu; Synology DSM; SMB/CIFS; backups | Migrated Plex from Fusco to Reese with careful preparation, backup and rollback planning, mount and path checks, and successful playback validation. | Completed and documented; the migration was successful and notably less dramatic than expected. | Confirmed | No |
| Operation No More Colon Crimes | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Fragment only | Yes |
| Operation Reception Desk | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Fragment only | Yes |
| Operation I Swear We Automated This | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Committee may have invented this | Yes, if evidence is recovered |
| Operation Bring Root Inside The Machine | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Fragment only | Yes |
| Operation DNS Shenanigans | Unknown | DNS; network | Recovered operation name; no reliable incident details recovered. | Unknown | Fragment only | Yes |

When more evidence is recovered, update the relevant row before creating a page from the [Operation Template](/Operations/Templates/Operation-Template).
