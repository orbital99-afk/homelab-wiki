---
title: Saturday Maintenance Runbook
description: Weekly checklist for keeping Reese and the wider homelab healthy.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Saturday Maintenance Runbook

## Operation Preventative Existential Crisis

> The goal is not to achieve enlightenment. The goal is to notice problems before they become a Tuesday night incident.

Run this checklist weekly or at the next sensible maintenance window. Record anything unusual before fixing it; mysteries are easier when the evidence has not been restarted.

## Ubuntu Updates — Has the OS Been Quietly Judging Us?

- [ ] Review available package updates on Reese.
- [ ] Apply routine security and package updates.
- [ ] Note whether a reboot is required and schedule it around active use.
- [ ] After rebooting, confirm Docker, mounts, and monitoring returned normally.

## Docker Container Status — Are the Little Boxes Still Alive?

- [ ] Check Shaw (Portainer) or Docker for stopped, restarting, or unhealthy containers.
- [ ] Review logs for unexpected failures rather than restarting on instinct.
- [ ] Confirm critical stacks use the expected compose configuration.

## Docker Image Updates / Diun — What Changed While Nobody Was Looking?

- [ ] Review Diun notifications.
- [ ] Read release notes for important or breaking changes.
- [ ] Confirm a current backup exists before updating stateful services.
- [ ] Update deliberately and validate each affected service.

## Disk Usage — Is Fusco Hoarding Again?

- [ ] Check filesystem usage, Docker growth, logs, and free space on Reese.
- [ ] Check relevant capacity and share availability on Fusco.
- [ ] Investigate unexpected growth before deleting data.

## UPS / Bear Status — Is the Emotional Support Battery Awake?

- [ ] Confirm Bear is online and NUT telemetry is current.
- [ ] Review battery charge, load, input voltage, and recent power events.
- [ ] Investigate stale telemetry or declining battery health.

## Backups — Can We Survive Reese Becoming Modern Art?

- [ ] Confirm the nightly `/opt/docker` rclone backup completed successfully.
- [ ] Confirm recent Daily HealthMonitor report zips are rotating correctly.
- [ ] Periodically inspect backup contents and perform a test restore.

## Plex / Arr Stack Spot Checks — Is the Entertainment Department Functional?

- [ ] Play a recent item in Plex and confirm its Fusco path is available.
- [ ] Check Sonarr, Radarr1080, Radarr4K, and Prowlarr health warnings.
- [ ] Submit or inspect a Seerr request and confirm routing is correct.
- [ ] Review failed imports, stuck queues, and indexer errors.

## Monitoring Dashboards — Are the Dashboards Lying or Merely Dramatic?

- [ ] Review Grafana trends for CPU, memory, disk, containers, temperatures, and Bear.
- [ ] Review Carter (Uptime Kuma) for degraded or paused checks.
- [ ] Confirm Prometheus targets are up and ntfy alerts can be delivered.

## Notes / Follow-up Jobs — Paperwork for Future Daniel

- [ ] Record anomalies, changes, and deferred work in The Library.
- [ ] Create a case file or operation for anything too large to solve safely during maintenance.
- [ ] Include owner, priority, and next action. “Future me will remember” is not a backup strategy.
