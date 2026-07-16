---
title: Operation Electrons Are A Privilege, Not A Right
description: Connect Bear to Reese with NUT and integrate UPS health into homelab monitoring.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Electrons Are A Privilege, Not A Right

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Status

Completed

## Mission Brief

Reese needed proper UPS visibility and automated monitoring instead of relying on hope, blinking lights, and emotional attachment to extension leads.

## Systems Involved

- Reese: 2012 Mac mini running Ubuntu Server
- Bear: USB-connected UPS
- NUT
- Prometheus
- Grafana
- HealthMonitor
- ntfy
- UPS exporter

> **Identity note:** Bear is the UPS. Carter is Uptime Kuma. Identity theft will not be tolerated in The Library.

## The Problem

- UPS status was not integrated into monitoring.
- Early reporting became unreliable.
- Bear did not provide an estimated runtime metric.
- A USB cable issue later caused incorrect or missing data.

## Investigation

- Confirmed USB HID device connectivity.
- Verified the NUT driver and service status.
- Used `upsc myups` to inspect available UPS values.
- Determined that the UPS hardware does not expose runtime.
- Replaced the USB cable when reporting became unreliable.

## Actions Taken

1. Installed and configured NUT.
2. Configured the UPS name as `myups`.
3. Enabled and verified `nut-server`, `nut-monitor`, and `nut-driver@myups`.
4. Confirmed that `upsc myups` returned live data.
5. Built or updated a UPS Prometheus exporter.
6. Added UPS metrics to HealthMonitor.
7. Added Grafana panels for UPS health.
8. Added notification support through ntfy.
9. Updated reporting after fitting a new USB cable.

### Known Values After Repair

| Metric | Value |
|---|---|
| Status | Online / `OL` |
| Battery | 100% |
| Load | Approximately 12% |
| Input voltage | Approximately 243 V |
| Runtime | Not reported by UPS |

## Outcome

- Bear became visible in HealthMonitor, Prometheus, and Grafana.
- Reese could report UPS status during normal operation.
- A later real power cut confirmed Reese and Bear remained running.
- Runtime remained unavailable as a native metric.

## Validation

- `upsc myups` returned live status.
- NUT services were active.
- The Prometheus exporter produced UPS metrics.
- HealthMonitor reported Bear as healthy.
- During the July 2026 power cut, Reese stayed online and battery data was captured.

## Casualties

- One suspicious USB cable.
- Several moments of believing the UPS was being deliberately unhelpful.
- Runtime graphs based on optimism rather than telemetry.

## Lessons for Future Daniel

- Test the cable before blaming the software stack.
- UPS runtime is hardware-dependent and may simply not exist.
- Validate backups and monitoring during a real outage when safely possible.
- Never assume `OL` means everything else is configured correctly.
- Exporter metrics should reflect what the device actually reports, not what we wish it reported.

## Best Quote

> “Electrons are a privilege, not a right.”

## Related Documentation

- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Canon](/Canon)
