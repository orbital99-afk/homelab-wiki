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

## Objective

Reese needed proper UPS visibility and automated monitoring instead of relying on hope, blinking lights, and emotional attachment to extension leads.

The Committee’s practical question was simple: could the homelab observe its own power situation without waiting for a dramatic outage to provide the answer?

## Background

The Library had long operated under the assumption that if the server stayed up, then the power story must be fine. That assumption was not robust, and in the hands of an overconfident operator it became a form of engineering folklore.

Bear, the UPS, was present and apparently willing to participate, but its status was not integrated into the monitoring stack. The result was a system that could be observed only through partial telemetry, suspicious cable behaviour, and the vague confidence of somebody who had already decided the hardware was probably fine.

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

## Phase 1: Establish a Reliable Power Narrative

The first task was to determine whether the UPS could be interrogated directly and whether the available values were usable in the monitoring stack.

- Confirmed USB HID device connectivity.
- Verified the NUT driver and service status.
- Used `upsc myups` to inspect available UPS values.
- Determined that the UPS hardware does not expose runtime.

## Phase 2: Integrate and Validate

Once the device could be queried, the next step was to make the information useful rather than merely available.

1. Installed and configured NUT.
2. Configured the UPS name as `myups`.
3. Enabled and verified `nut-server`, `nut-monitor`, and `nut-driver@myups`.
4. Confirmed that `upsc myups` returned live data.
5. Built or updated a UPS Prometheus exporter.
6. Added UPS metrics to HealthMonitor.
7. Added Grafana panels for UPS health.
8. Added notification support through ntfy.
9. Updated reporting after fitting a new USB cable.

## Notable Findings

- The UPS status was not integrated into monitoring at the outset, which made the system appear more mysterious than it was.
- Bear did not provide an estimated runtime metric. This was not a software failure. It was a hardware limitation, which is the most irritating kind.
- A suspicious USB cable later caused incorrect or missing data. The Committee does not formally endorse blaming the cable first, but it is difficult to deny that the cable was very much in the room.
- A real power cut later confirmed that Reese and Bear remained running. This was useful, although it was unfortunately not dramatic enough to satisfy the Committee’s appetite for spectacle.

## Outcome

- Bear became visible in HealthMonitor, Prometheus, and Grafana.
- Reese could report UPS status during normal operation.
- A later real power cut confirmed Reese and Bear remained running.
- Runtime remained unavailable as a native metric.

## Mission Status

COMPLETED

## Validation

- `upsc myups` returned live status.
- NUT services were active.
- The Prometheus exporter produced UPS metrics.
- HealthMonitor reported Bear as healthy.
- During the July 2026 power cut, Reese stayed online and battery data was captured.

### Known Values After Repair

| Metric | Value |
|---|---|
| Status | Online / `OL` |
| Battery | 100% |
| Load | Approximately 12% |
| Input voltage | Approximately 243 V |
| Runtime | Not reported by UPS |

## Lessons Learned

- Test the cable before blaming the software stack.
- UPS runtime is hardware-dependent and may simply not exist.
- Validate backups and monitoring during a real outage when safely possible.
- Never assume `OL` means everything else is configured correctly.
- Exporter metrics should reflect what the device actually reports, not what we wish it reported.
- A monitoring system that only works when everything is calm is still a monitoring system, but it is not a good one.
- The Committee has learned that “power is fine” becomes significantly more convincing once it is backed by evidence instead of faith.

## Official Findings

After review of USB connectivity, NUT configuration, exporter output, dashboard visibility, and the later real power-cut event, the Committee found that Reese and Bear were operating with improved observability and that the UPS status was now properly represented in the monitoring system.

The Committee also formally noted that the UPS did not expose runtime values, and that this absence was a hardware characteristic rather than an implementation failure.

## Committee Findings

### Root

> “We now have a UPS that reports its own existence, which is already more than we had before.”

### Finch

> “And the cable?”

### Bear

> “I was available the whole time. I was simply waiting for a system that would ask the right question.”

### Health & Safety

> “Approved, provided the outage remained accidental and not theatrical.”

### Finance Department

> “This was an expensive way to discover that a battery does not come with a prophecy engine.”

## Final Verdict

Bear was found:

- Not dead
- Not haunted
- Not secretly trying to sabotage Reese
- Not currently able to provide runtime as a native metric
- Merely more visible than before, and considerably less mysterious

## Follow-On Operations

- Continue monitoring Bear and associated UPS metrics through HealthMonitor, Prometheus, Grafana, and ntfy.
- Continue validating monitoring behaviour during real power events when safely possible.

## Series Status

This operation was renewed for another season after investigators discovered that power monitoring is not a one-off problem and that electricity remains deeply uninterested in the operator’s emotional needs.

## Best Quote

> “Electrons are a privilege, not a right.”

## Related Documentation

- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Canon](/Canon)
