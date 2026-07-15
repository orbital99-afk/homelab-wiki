---
title: Monitoring Runbook
description: Health checks and recovery notes for metrics, availability, alerts, and daily reports.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Monitoring Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

Monitoring establishes whether services are alive, healthy, or slowly cooking. Prometheus collects metrics; Grafana displays them; Carter checks availability; exporters describe Reese, containers, cupboard temperature, and Bear; ntfy delivers alerts; Diun watches images; and the Daily HealthMonitor report provides a scheduled summary.

## Where It Lives

- Most monitoring services run as Docker containers on Reese.
- Glances, cAdvisor, node_exporter, the cupboard temperature exporter, and the UPS exporter provide source data.
- Uptime Kuma is Carter; the UPS is Bear.
- Configuration and persistent data generally live beneath `/opt/docker`.

## Quick Health Check

```bash
docker ps
docker logs --tail=100 <container>
cd "<appropriate-compose-directory>"
docker compose ps
df -h
```

Check Prometheus targets, current Grafana data, Carter's active checks, Glances host metrics, cupboard temperatures, Bear telemetry, ntfy delivery, Diun notices, and the latest Daily HealthMonitor report. Stale data may mean an exporter is down even when Grafana is beautifully rendering yesterday.

## Restart Procedure

1. Identify whether the failure is collection, storage, display, checking, or notification.
2. Inspect the affected container's logs and dependencies.
3. Change into the correct monitoring compose directory before using Compose commands.
4. Restart only the affected service with `docker compose restart <service>` or `docker restart <container>`.
5. Confirm fresh timestamps, healthy Prometheus targets, active Carter checks, and alert delivery.

## Common Goblins

- **Exporter failure:** One dashboard panel is stale while the rest remain current.
- **Storage pressure:** Prometheus or Grafana becomes unhealthy as disk space disappears.
- **DNS Goblin:** Scrape targets or notification endpoints cannot resolve.
- **Permission Goblin:** A service cannot access its data or configuration.
- **Alert silence:** Metrics exist, but ntfy or Carter notifications do not arrive.
- **Update Goblin:** A changed image or metric name breaks dashboards and scrape jobs.

## Do Not Casually Delete

Do not delete Prometheus data, Grafana dashboards, Carter checks, notification configuration, exporter configs, or Daily HealthMonitor history without a backup and a reason. Historical metrics are evidence; deleting them during an incident is helping the goblin.

## Related Pages

- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Backups Runbook](/Runbooks/Backups)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Known Goblins](/Case-files/Known-Goblins)
