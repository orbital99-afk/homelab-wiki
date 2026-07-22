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
| [Operation I Swear We Automated This](/Operations/Operation-i-swear-we-automated-this) | Unknown | Reese; monitoring stack; systemd; cron; Prometheus; Grafana; HealthMonitor | Investigated why monitoring exporters and scripts worked when launched manually but did not persist reliably across reboot or automation. | Completed and documented; persistence was formalised through service management and reboot validation. | Confirmed | No |
| [Operation The Fan Was Fine, Ubuntu Was Just Vibes](/Operations/Operation-the-fan-was-fine-ubuntu-was-just-vibes) | Approximately one to two weeks after the earlier environmental operation | Reese; Ubuntu; macfanctld; fan control; monitoring | Reopened the thermal investigation after CPU temperatures exceeded 100°C and identified the missing Apple-specific fan-control layer under Ubuntu. | Completed and documented; temperatures fell dramatically after macfanctld was installed and enabled. | Confirmed | No |
| [Operation The Router Has Decided Who Deserves Bandwidth](/Operations/Operation-the-router-has-decided-who-deserves-bandwidth) | Unknown | Router; QoS; network performance; traffic shaping | Enabled a QoS feature intended to improve performance, then observed that it decreased throughput until it was disabled. | Completed and documented; disabling QoS restored normal performance and the router stopped overmanaging packets. | Confirmed | No |
| [Operation No More Colon Crimes](/Operations/Operation-no-more-colon-crimes) | Unknown | Reese; Docker; DNS; Caddy; Elias / Tailscale; MagicDNS; web services | Documented the intended move from raw host-and-port navigation to friendly local or tailnet service names. | Active foundation completed; DNS, routing, and per-client validation remain ongoing. | Confirmed architecture | No |
| [Operation Reception Desk](/Operations/Operation-reception-desk) | Unknown | Reese; Caddy; Docker; DNS; Elias / Tailscale; web services | Documented Caddy's intended role as the hostname-aware reverse proxy between friendly names and backend services. | Active foundation completed; deployment, configuration backup, resilience, and per-route validation remain active or planned. | Confirmed architecture | No |
| [Operation: The Thirty-Six-Hour Goal That Was Scored, Rescinded, Scored Again, and Eventually Entered Library Folklore](/Operations/Operation-the-thirty-six-hour-goal) | July 2026 | Reese; local snapshots; OneDrive; rclone; tar; zstd; HealthMonitor | Reconstructed the original slow-backup match footage and documented the redesign from thousands of loose objects to one compressed weekly off-site archive. | Completed and documented; backup and HealthMonitor semi-finals won, Library grand-final goal awarded. | Confirmed | No |
| Operation I Swear We Automated This | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Committee may have invented this | Yes, if evidence is recovered |
| Operation Bring Root Inside The Machine | Unknown | Unknown | Recovered operation name; details not yet recovered. | Unknown | Fragment only | Yes |
| Operation DNS Shenanigans | Unknown | DNS; network | Recovered operation name; no reliable incident details recovered. | Unknown | Fragment only | Yes |

When more evidence is recovered, update the relevant row before creating a page from the [Operation Template](/Operations/Templates/Operation-Template).
