---
title: Operation I Swear We Automated This
description: Document the monitoring stack persistence work for Reese, including custom exporters, service management, reboot testing, and the recurring lesson that running is not the same as automated.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation I Swear We Automated This

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Objective

Make Reese’s custom monitoring exporters and scripts start automatically, survive reboots, recover reliably, and stop depending on Finch remembering to launch them manually.

The practical goals were straightforward:

- run without an interactive terminal
- start after boot
- restart after failure where appropriate
- expose expected metrics consistently
- allow Prometheus and HealthMonitor to depend on them
- be inspectable through standard service-management tools
- eliminate “it worked yesterday” as a deployment strategy

The central question was:

> “Did we automate this, or did we merely run it once and become emotionally attached to the result?”

## Background

The environmental and UPS monitoring stack began as a set of useful components with real value. The Arduino R3 and two DS18B20 sensors produced environmental data. Metrics were collected for cupboard temperature, room temperature, and the temperature delta later known as the Reese Baking Index. A custom cupboard temperature exporter exposed metrics on port 9200. A custom UPS exporter exposed Bear’s metrics on port 9201. Prometheus scraped the exporters. Grafana displayed the metrics. HealthMonitor used related metrics and scripts.

The components were technically useful. They produced data. Grafana panels showed values. Prometheus received them. The Committee declared success.

Then Reese rebooted, or a process stopped, and certain parts of the monitoring stack vanished. The Committee discovered an important distinction:

- manually started
- currently running
- configured as a service
- enabled at boot
- actually persistent

These states were not interchangeable. The exporters had achieved existence but not permanence. The Committee had mistaken “running now” for “will run later.” Root had used the word automated with insufficient legal precision.

## Phase 1: It Works

The first phase was the one that made the later confusion possible. The custom scripts and exporters were created, and they worked when launched manually. Metrics appeared. Prometheus could scrape them. Grafana displayed meaningful data. HealthMonitor could consume relevant information. Finch and Root celebrated the progress.

The monitoring stack looked automated. The problem was that it had only achieved the first half of automation: it worked in the moment.

## Phase 2: It No Longer Works

The next phase began when one or more monitoring components were not present after reboot or were not running unless launched manually.

The symptoms varied. Some were practical and some were merely emotionally irritating:

- missing Prometheus targets
- absent cupboard metrics
- absent UPS metrics
- Grafana panels showing no data
- scripts working when manually executed
- terminal sessions having previously kept processes alive
- services existing but not being enabled
- service definitions requiring correction
- automation calling an old script or path

The central clue was simple:

> The command worked manually.

The central problem was equally simple:

> Finch was not interested in manually running it forever.

## Phase 3: The Automation Interrogation

The Committee then switched from celebration to inspection. The question became whether the relevant components were truly automated, or merely available when somebody launched them manually and then forgot about the session.

The investigation covered standard service and process checks:

- inspect running processes
- inspect systemd service status
- inspect whether services are enabled
- review service definitions
- confirm working directories and executable paths
- inspect logs
- test exporters locally
- distinguish a failed service from a service that was never enabled
- confirm Prometheus target health
- check whether cron or another scheduler referenced an obsolete script

Safe generic commands were used to inspect behaviour:

```bash
systemctl status <service>
systemctl is-enabled <service>
journalctl -u <service> --no-pager
sudo systemctl daemon-reload
sudo systemctl enable --now <service>
curl http://localhost:<port>/metrics
ps aux | grep <process>
```

The Committee also revisited the recurring automation problem documented elsewhere: the intended daily report script had moved to `~/health/daily-report.sh`, but cron continued using `~/daily-health.sh`. This was not a new mystery. It was a familiar one, and it demonstrated that automation obeys the exact path given to it.

## Phase 4: Systemd Enters the Committee

The move from manually launched processes to proper service management was the point at which the operation stopped being a casual script improvement and became a formal service persistence effort.

The work generally involved:

1. Create or correct service unit definitions.
2. Set the correct executable and working directory.
3. Confirm the appropriate user.
4. Add restart behaviour where suitable.
5. Reload systemd.
6. Enable the service.
7. Start the service.
8. Inspect status and logs.
9. Test the metrics endpoint.
10. Reboot and verify the service returns.

This phase was important because it established the distinction between a process that exists and a process that has been granted the right to survive reboot. Creating a unit file does not enable it. Starting a service does not necessarily enable it. Enabling a service does not prove that it starts successfully. A green status before reboot is not the final validation. The reboot test is where automation receives its citizenship exam.

Systemd was treated as a formal and humourless department. It accepted only correct instructions and refused to infer intent from enthusiasm.

## Phase 5: The Reboot Trial

The decisive validation came from rebooting Reese and confirming that the relevant services returned without manual intervention.

The Committee watched with unnecessary tension as the host restarted. The questions were simple and costly to the nerves:

- Did the exporter processes return?
- Did the metrics endpoints respond?
- Did Prometheus see the targets again?
- Did Grafana receive data again?
- Did HealthMonitor have the expected information again?

This was the point where theoretical automation became practical automation. A service that worked before reboot but failed afterwards was not considered complete. A service that survived the reboot was considered to have passed the test.

## Phase 6: The Old Path Returns

The operation also reaffirmed the recurring lesson that automation does not understand that a newer script exists. It only understands the exact path written in its configuration.

The daily report example is the clearest case. The intended script had moved to `~/health/daily-report.sh`, but cron still called `~/daily-health.sh`. The result was not a philosophical failure of automation. It was a straightforward one: a replacement script did not automatically replace every caller that had been configured earlier.

The same lesson applied to the monitoring stack. A service definition, cron entry, or wrapper script that still pointed at the old location could silently defeat a supposedly improved setup.

## Systems Involved

- Reese
- Ubuntu Server
- systemd
- cron
- Prometheus
- Grafana
- HealthMonitor
- cupboard temperature exporter
- UPS exporter
- Arduino R3 monitoring platform
- dual DS18B20 sensors
- Bear / NUT monitoring
- custom shell and Python scripts where appropriate
- Committee confidence

## Technical Root Cause

The monitoring components had initially achieved functional operation, but persistence and automated startup had not been fully established or consistently validated.

Likely classes of issue included:

- processes started manually
- service units not yet created
- service units created but not enabled
- incorrect service paths or working directories
- old automation still referring to superseded scripts
- insufficient reboot validation

The broader root cause was treating “it runs” as equivalent to “it is automated.”

## Actions Taken

1. Identified scripts and exporters that depended on manual startup.
2. Reviewed existing systemd and cron configuration.
3. Created or corrected systemd service definitions.
4. Confirmed executable paths and working directories.
5. Reloaded systemd configuration.
6. Enabled and started required services.
7. Inspected service status and logs.
8. Tested local metrics endpoints.
9. Confirmed Prometheus target health.
10. Rebooted Reese.
11. Verified services returned without manual intervention.
12. Updated obsolete automation references where discovered.
13. Documented the persistence requirements in The Library.

## Validation

The following were verified as part of the operation:

- custom exporters ran under service management
- services were enabled where required
- metrics endpoints responded
- Prometheus could scrape expected targets
- Grafana received data again
- monitoring survived reboot
- manual terminal sessions were no longer required for the relevant services
- cron or service paths were corrected where obsolete references were found

## Outcome

- the custom monitoring components became persistent
- systemd managed the relevant exporter processes
- monitoring returned automatically after reboot
- Prometheus and Grafana no longer depended on Finch manually launching scripts
- the distinction between running, enabled, and persistent became official Library doctrine
- later automation work benefited from the lessons learned

## Mission Status

COMPLETED — PERSISTENCE ACHIEVED

> Automation remains subject to periodic verification because configuration drift also believes in persistence.

## Coffee Status

- Initial exporter test: Optimistic cup
- First reboot: Cup placed within immediate reach
- Missing metrics discovered: Second cup authorised
- systemd investigation: Coffee cooling beside terminal
- Successful reboot validation: Victory coffee
- Discovery of an old cron path later: Coffee replaced with interpretive swearing

## Casualties

- one or more manually launched processes
- confidence in the phrase “it should start automatically”
- several terminal tabs
- at least one old path
- one assumption that creating a service meant enabling it
- no exporters permanently lost
- no sensors harmed
- Finch’s willingness to accept the word “automated” without evidence

## Lessons Learned

- running is not the same as automated
- started is not the same as enabled
- enabled is not the same as healthy
- healthy before reboot is not the same as persistent
- reboot validation matters
- inspect service logs
- use absolute paths in automation where appropriate
- update every caller when moving a script
- verify Prometheus targets after changes
- document custom services and ports
- manual success proves the code can run, not that deployment is correct
- automation should survive the operator leaving the room
- a terminal window is not an orchestration platform
- systemd will not infer intent from enthusiasm
- cron remains fiercely loyal to obsolete paths
- the phrase “we automated this” now requires supporting evidence
- Root’s definition of automated was temporarily found to mean “Finch ran it twice”
- Reese cannot be expected to remember a process that existed only because a shell was still open
- every custom exporter eventually demands paperwork
- the reboot test is where confidence goes to court

## Official Findings

The Committee concluded that the monitoring code was functional, but persistence was initially incomplete. The Committee had declared automation prematurely, based on the fact that the components worked when launched manually. Systemd service management corrected the persistence problem. Reboot testing provided the decisive evidence that the services could recover without manual intervention. Old script references remained a recurring risk. Finch was justified in repeatedly asking whether the work had already been automated. Root was technically correct that automation existed conceptually, but operationally incorrect because concepts do not start after reboot.

## Committee Findings

### Finch

> “I thought we automated this.”

### Root

> “We did, conceptually.”

### Finch

> “Then why is it not running?”

### Root

> “Because automation is a mood until a service unit exists and a reboot confirms it.”

### systemd

> “No enabled unit was found.”

### cron

> “I ran exactly the old path provided.”

### Prometheus

> “Target down.”

### Grafana

> “I can only draw the nothing I receive.”

### Reese

> “I rebooted. The shell process did not.”

### Health & Safety

> “Please define automated before using the word again.”

## Official Automation Scale

### Level 0 — Theoretical
Someone discussed automation.

### Level 1 — Manual With Confidence
The command works when Finch runs it.

### Level 2 — Scripted
A script exists.

### Level 3 — Service-Shaped
A service file exists somewhere.

### Level 4 — Enabled
The service is configured to start automatically.

### Level 5 — Reboot Proven
Reese restarts and the service returns without assistance.

### Level 6 — Library Certified
The service survives reboot, produces expected output, has logs, monitoring, and documentation.

Operation I Swear We Automated This moved the relevant monitoring components toward Level 6.

## Final Verdict

### The monitoring stack was found:

- Functional
- Useful
- Previously dependent on optimism
- Insufficiently persistent
- Recoverable
- Capable of surviving reboot once properly configured
- Finally automated in the legally defensible sense

### systemd was found:

- Formal
- Exact
- Unimpressed by intent
- Willing to help after receiving correct paperwork
- Not responsible for services nobody enabled
- The closest thing Reese has to a civil service

### Cron was found:

- Punctual
- Obedient
- Completely indifferent to newer scripts
- Still using the path it was given
- Innocent of creativity
- Guilty of loyalty

### Root was found:

- Enthusiastic
- Conceptually correct
- Operationally premature
- Too willing to declare victory before reboot
- Required to provide future evidence when using the word automated

### Finch was found:

- Correctly suspicious
- Increasingly caffeinated
- Entitled to ask the title question
- No longer willing to accept “it worked manually” as closure

## Best Quote

> “The automation was real. Its persistence was theoretical.”

> “I swear we automated this.”

## Follow-On Operations

- [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report)
- [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked)
- [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right)
- ongoing Saturday maintenance
- documenting all custom services and exporter ports
- checking service persistence after future reboots
- monitoring power-cut behaviour
- ensuring backup and restore procedures include custom service definitions

## Series Status

Operation I Swear We Automated This was commissioned as a mystery series. Every episode began with Finch saying the system had worked yesterday. The villain was repeatedly revealed to be missing persistence, an old path, or an unenabled service. The series was renewed because custom infrastructure keeps producing sequels. Systemd declined an interview because no correctly formatted unit file had been supplied.

## Related Documentation

- [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked)
- [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right)
- [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report)
- [Operation Preventative Existential Crisis](/Operations/Operation-preventative-existential-crisis)
- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Saturday Maintenance Runbook](/Operations/Saturday-Maintenance-Runbook)
- [Operation Archive](/Operations/Operation-Archive)
- [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox)
- [Canon](/Canon)
