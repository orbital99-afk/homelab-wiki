---
title: Monitoring
description: Overview of homelab metrics, availability checks, alerting, and daily health reporting.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Monitoring

Monitoring answers three questions: is it up, is it healthy, and is Reese being slowly baked in the garage cupboard?

## Metrics and Dashboards

- **Prometheus** collects time-series metrics from Reese and supporting exporters.
- **Grafana** turns those metrics into dashboards and trends.
- **Glances** provides a fast live view of host resources.
- **cAdvisor** exposes Docker container resource usage.
- **node_exporter** exposes Ubuntu host metrics such as CPU, memory, filesystems, and network activity.
- The **cupboard temperature exporter** reports environmental and hardware temperature data.
- The **UPS exporter** reports Bear's battery, load, voltage, and online state from NUT data.

## Availability and Alerts

- **Uptime Kuma / Carter** checks whether services and endpoints are reachable.
- **ntfy** delivers actionable notifications from monitoring and scheduled jobs.
- **Diun** watches Docker images and reports available updates. It announces work; it does not prove an update is safe.

## Daily Reporting

The Daily HealthMonitor report provides a scheduled summary of system health. Recent reports are retained as rotated zip files for comparison and incident review.

## Operating Guidance

An alert is a starting point, not a diagnosis. Check correlated Grafana metrics, container status, logs, Fusco mounts, and Bear telemetry before changing anything. After an incident, capture the cause and corrective action in The Library so Root does not have to rediscover the same mystery next month.
