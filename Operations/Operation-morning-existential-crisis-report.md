---
title: Operation Morning Existential Crisis Report
description: Create and repair the automated daily HealthMonitor report for the homelab.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Morning Existential Crisis Report

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

> **Recurring warning:** Cron does not understand intent. Cron understands paths and betrayal.

## Status

Completed

## Objective

Create a daily report that tells Daniel whether Reese and the surrounding homelab survived the night without requiring an immediate tour of dashboards, terminals, and suspicious blinking lights.

The mission was not merely to generate data. It was to turn a scattered collection of health signals into a single, semi-coherent morning briefing.

## Background

The homelab health information had spread itself across multiple tools, leaving the operator to interpret a mosaic of dashboards, logs, and half-remembered terminal output. The Committee therefore authorised the creation of a daily summary that could be read once, understood once, and then used as evidence in the next crisis.

This became urgent when the report system revealed that cron had continued to call an older script path despite the intended replacement already existing. The problem was therefore both technical and philosophical: automation was doing the wrong thing with complete confidence.

## Systems Involved

- Reese
- HealthMonitor
- Ubuntu cron
- Docker
- Bear / NUT
- Disk monitoring
- Backups
- Daily ZIP reports
- Email and ntfy notifications
- Prometheus / Grafana where relevant

## Phase 1: Audit the Broken Morning Routine

The first step was to inspect the existing daily report scripts and determine where the automated process had diverged from the intended workflow.

- Reviewed the existing daily report scripts.
- Discovered that cron was still using `~/daily-health.sh`.
- Confirmed that the intended replacement was `~/health/daily-report.sh`.
- Checked report generation, ZIP creation, and delivery.
- Verified that Bear runtime was unavailable because the UPS does not expose it.

## Phase 2: Restore the Daily Report

Once the cause of the drift was clear, the report itself was repaired and reintroduced as an automated process.

1. Created or improved the HealthMonitor daily report.
2. Included Ubuntu update status.
3. Included Docker running and stopped container status.
4. Included disk usage.
5. Included Bear UPS status.
6. Included backup status and an overall health summary.
7. Moved the active report script to `~/health/daily-report.sh`.
8. Updated cron to use the new script.
9. Added daily ZIP output.
10. Added 14-day report rotation.
11. Verified email delivery.
12. Later added ntfy notification support.
13. Updated Bear metrics after the USB cable replacement.

## Notable Findings

- Cron was not broken in a dramatic sense. It was merely obeying the wrong script with perfect loyalty.
- The report became a morning crisis summary rather than a manual pilgrimage through multiple dashboards.
- ZIP files were used as sealed evidence packets for the daily health record. The Committee found this both practical and faintly theatrical.
- The UPS runtime metric remained unavailable. This was not a surprise but it did become part of the daily report’s emotional tone.
- The phrase “working manually” became less useful once the automation path was corrected.

## Outcome

- Reese produces a daily homelab health report automatically.
- Reports are packaged into ZIP files.
- Old reports are rotated.
- The report became a morning summary rather than a manual dashboard pilgrimage.
- Cron now uses the correct script.

## Mission Status

COMPLETED

## Validation

- Manual report generation succeeded.
- The scheduled report ran from cron.
- Email delivery worked.
- ntfy notifications worked.
- Generated reports reflected current Bear and Docker status.

### Example Healthy Output

| Metric | Value |
|---|---|
| Health | Healthy |
| Battery | 100% |
| Load | Approximately 12% |
| Input | Approximately 243 V |
| UPS status | Online / `OL` |
| Runtime | Not reported by UPS |

## Lessons Learned

- After replacing a script, check cron, systemd timers, aliases, and old paths.
- A working manual command does not prove automation is using it.
- Keep report retention bounded.
- Include enough information to diagnose, not just enough to cause panic.
- Cron is loyal to the exact typo you gave it.
- A report that runs on time is useful; a report that is ignored is merely decorative.
- The phrase “I’ll just check it manually” is not a substitute for automation when the automation is already running and still wrong.

## Official Findings

The Committee determined that the daily health report had been successfully restored as an automated morning briefing for Reese and the surrounding homelab. The report now covers the relevant operational domains, including Ubuntu, Docker, disk usage, Bear, backups, and delivery channels.

The Committee further found that cron had been corrected to invoke the intended script and that the reporting process now operates with suitable retention, packaging, and notification behaviour.

## Committee Findings

### Root

> “The report is now automated, which means I no longer have to explain the same dashboard to the same person every morning.”

### Finch

> “And the old script?”

### Cron

> “I executed the path provided. I did not infer intent.”

### Reese

> “I survived another night. Please stop making this sound so dramatic.”

### Health & Safety

> “Approved, provided the report remains informative and does not trigger an immediate incident response every morning.”

## Final Verdict

The morning report was found:

- Not cursed
- Not sentient
- Not secretly reporting on the operator’s sleep habits
- Merely reliable enough to be useful

## Follow-On Operations

- Continue using the daily report as the standard morning summary for the homelab.
- Continue validating notification delivery and retention behaviour as part of routine maintenance.

## Series Status

This operation was renewed for another season after investigators confirmed that mornings remain a recurring problem and that the report is now a reliable companion to the inevitable crisis.

## Best Quote

> “Good morning. Here is today’s automated existential crisis.”

## Related Documentation

- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Backups Runbook](/Runbooks/Backups)
- [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right)
