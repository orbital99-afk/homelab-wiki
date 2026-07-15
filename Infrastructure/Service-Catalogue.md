---
title: Service Catalogue
description: Practical catalogue of homelab services, locations, purposes, and access notes.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Service Catalogue

This is the quick answer to “what is that container, and will anyone notice if it stops?” Access details should be verified against the current compose files and Zoe before changing ports or URLs.

| Service | Codename | Host | Purpose | Notes |
|---|---|---|---|---|
| Plex | — | Reese | Streams the media libraries stored on Fusco | Validate Fusco mounts before blaming Plex |
| Sonarr | — | Reese | Manages television acquisition and organisation | Part of the Arr stack |
| Radarr1080 | — | Reese | Manages 1080p film acquisition | Separate profile and library from 4K |
| Radarr4K | — | Reese | Manages 4K film acquisition | Keep paths and quality profiles distinct |
| Prowlarr | — | Reese | Central indexer management for the Arr stack | Check integrations after credential changes |
| Jellyseerr / Seerr | — | Reese | Handles user media requests | Confirm requests reach the correct Sonarr or Radarr instance |
| Kometa | — | Reese | Maintains Plex collections and metadata | Scheduled automation; configuration is important backup data |
| Tautulli | — | Reese | Reports Plex activity and usage | Useful for playback troubleshooting |
| Portainer | Shaw | Reese | Manages Docker stacks and containers | Bring up early during recovery |
| Homepage | Zoe | Reese | Dashboard and service launcher | Friendly front door, not the documentation system |
| Uptime Kuma | Carter | Reese | Performs availability checks and status monitoring | Carter is never the UPS |
| Prometheus | — | Reese | Scrapes and stores monitoring metrics | Preserve scrape configuration and data-retention choices |
| Grafana | — | Reese | Displays dashboards and metrics | Friendly-name goal: `grafana.reese` |
| Glances | — | Reese | Shows host-level resource health | Useful for rapid live diagnosis |
| cAdvisor | — | Reese | Exposes container resource metrics | Prometheus scrape target |
| node_exporter | — | Reese | Exposes Ubuntu host metrics | Prometheus scrape target |
| ntfy | — | Reese | Delivers homelab notifications | Used by monitoring and scheduled jobs |
| Wiki.js | The Library | Reese | Stores homelab documentation and runbooks | PostgreSQL-backed; protect both application and database data |
| Tailscale | Elias | Reese and authorised devices | Provides private remote access | Preferred remote-access path |
| NUT | Bear monitoring | Reese / UPS connection | Collects UPS state and battery telemetry | Bear is the physical UPS; NUT supplies its telemetry |

## Committee Notes

- **Plex:** The theatre.
- **Sonarr:** TV acquisition goblin.
- **Radarr1080:** Sensible movie department.
- **Radarr4K:** Show pony division.
- **Prowlarr:** Index whisperer.
- **Jellyseerr / Seerr:** Request desk with veto power.
- **Kometa:** Poster fashion crimes, but intentional.
- **Tautulli:** Who watched what, and why are they like this?
- **Portainer / Shaw:** Container bouncer.
- **Uptime Kuma / Carter:** Alive/dead detective.
- **Homepage / Zoe:** Reception desk.
- **Prometheus:** Metric hoarder.
- **Grafana:** Pretty panic.
- **ntfy:** Phone yelling service.
- **Wiki.js / The Library:** Memory palace with Markdown shelves.
- **Tailscale / Elias:** Creepy van network, but secure.

Most applications run as Docker containers on Reese. Fusco supplies storage and media shares; it is not a convenient place to improvise application changes.
