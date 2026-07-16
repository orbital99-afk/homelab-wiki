---
title: Operation The Fan Was Fine, Ubuntu Was Just Vibes
description: Document the thermal investigation of Reese after CPU temperatures exceeded 100°C, including the macfanctld fix and the formal clearing of the cupboard and fan.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation The Fan Was Fine, Ubuntu Was Just Vibes

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Objective

Determine why Reese, the 2012 Mac mini running Ubuntu Server, was reaching extreme CPU temperatures despite the earlier environmental investigation concluding that the cupboard was operating within safe conditions.

The practical objectives were simple and urgent:

- confirm the CPU temperature readings
- determine whether the internal fan was operating
- rule out environmental causes
- investigate airflow, hardware, sensors, thermal management, and fan control
- prevent thermal damage
- restore stable operating temperatures
- document the cause and fix
- avoid replacing innocent hardware

The central contradiction was this:

The cupboard was fine.

Reese was not.

## Background

Operation Is Reese Being Slowly Baked? had already established the relevant environmental baseline. That earlier operation had installed environmental sensors, measured cupboard and room temperatures, created the Reese Baking Index, established long-term environmental visibility, and concluded that the cupboard was not slowly baking Reese.

The Committee had therefore closed the thermal case with considerable confidence.

Approximately one to two weeks later, unexpectedly high CPU temperatures were discovered. CPU temperatures exceeded 100°C before the fix. This created an immediate institutional crisis because the environmental suspect had already been cleared. The Committee reopened the case under the assumption that either:

- the previous case had missed something
- the fan had failed
- Reese had developed a new thermal problem
- physics had changed its position
- or someone had misunderstood what “the cupboard is fine” actually meant

The CPU was treated as the victim. The Mac mini was treated as the crime scene. The cupboard was treated as a previously cleared suspect dragged back in for questioning.

## Case Reopened

The investigation reopened as a formal thermal inquiry.

### Incident Summary

- Scene: Reese
- Location: garage cupboard
- Victim: CPU thermal stability
- Primary symptom: temperature exceeding 100°C
- Previously cleared suspect: cupboard environment
- Lead investigator: Root
- Concerned operator: Finch
- Person of interest: internal fan
- Actual culprit: absent or insufficient Apple-specific fan control under Linux
- Time to generate absurd theories: immediate
- Time to identify the likely cause once examined: embarrassingly short

## Act I: Discovery of the Crime Scene

The high CPU temperature was noticed during routine monitoring. There was immediate disbelief because the cupboard sensors had looked healthy. The environmental data said the room and cupboard were not the problem. The Committee therefore had to confront the uncomfortable distinction between ambient temperature and component temperature.

The room was fine. The CPU was not.

The initial suspicion was that the internal fan had failed. That was the obvious suspect and also the most dramatic one. Finch considered whether Reese had silently been cooking itself inside the cupboard. Root, by contrast, became alarmingly calm, which is often how the serious investigators behave right before the case turns into a software issue.

The cupboard sensors had accurately reported that the environment was acceptable. They had not promised that the CPU was fine.

## Act II: The Suspect Board

The Committee assembled a list of plausible and absurd hypotheses.

### Reasonable Suspects

- failed internal fan
- fan not spinning fast enough
- dust or restricted airflow
- dried or ageing thermal paste
- blocked vent
- heavy CPU load
- incorrect sensor reading
- Apple hardware thermal-management mismatch under Linux
- missing fan-control software
- service not running
- cupboard airflow issue despite acceptable ambient temperature

### Committee-Approved Hypotheses

The absurd hypotheses were numerous and, in some cases, professionally unhelpful:

- Reese was mining cryptocurrency without authorisation
- Fusco had redirected excess heat out of professional jealousy
- Bear was charging Reese through emotional proximity
- the aluminium chassis had entered a self-toasting cycle
- the CPU was attempting atmospheric re-entry
- the cupboard was innocent during daylight hours but malicious after midnight
- a rogue Docker container had discovered fire
- Apple had hidden a small ceremonial furnace in the 2012 model
- the Reese Baking Index had become self-fulfilling
- Grafana had made the temperature higher by observing it
- the fan had joined a union and was awaiting approved working conditions
- Ubuntu believed thermal management was a personal choice
- Root had accidentally enabled “prestige disaster mode”
- Finch’s earlier decision to build sensors had offended the laws of irony

These were jokes. They were not the technical conclusion. The technical conclusion was much less theatrical and far more useful.

## Act III: Crime Scene Examination

The practical investigation focused on whether the high temperature was caused by environmental conditions, fan failure, or inadequate thermal management under Linux.

The committee reviewed the available system evidence and hardware context:

- confirm CPU temperature readings using available system tools
- inspect CPU load
- inspect fan RPM if available
- listen for fan behaviour
- inspect airflow and vents
- confirm the cupboard ambient temperature remained reasonable
- review whether Linux was controlling the fan correctly
- check for Apple-specific fan-control tooling
- inspect service status once macfanctld was considered
- distinguish a dead fan from a fan that was simply not being actively managed

Safe generic commands were used where useful:

```bash
sensors
top
htop
systemctl status macfanctld
journalctl -u macfanctld --no-pager
```

The evidence quickly began pointing away from:

- cupboard temperature
- catastrophic fan hardware failure
- rogue workload

And toward:

- missing or inadequate fan-control behaviour under Ubuntu

## Act IV: The Almost Immediate Breakthrough

The investigation had been prepared for hardware surgery, replacement fans, thermal-paste operations, chassis disassembly, airflow redesign, a full environmental tribunal, possible relocation of Reese, and several days of dramatic uncertainty.

Instead, the key question became:

> “Is anything actually managing the fan?”

The answer revealed the case.

Ubuntu was running successfully on the Mac mini. The fan hardware existed and was functional. Apple-specific thermal and fan-control behaviour was not being handled in the expected way by default. The missing layer was suitable fan management for the Apple hardware.

The case was therefore downgraded from attempted murder to management failure.

## Act V: macfanctld Enters the Scene

The fix was to install and configure macfanctld so that the Apple hardware received appropriate fan management under Linux.

The practical sequence was:

1. Identify macfanctld as the appropriate fan-control service.
2. Install it.
3. Configure it appropriately.
4. Start and enable the service.
5. Confirm the service was active.
6. Observe fan response.
7. Monitor CPU temperature.
8. Confirm temperatures fell.
9. Verify normal operation over time.
10. Ensure persistence after reboot where appropriate.

After macfanctld began managing the fan:

- fan behaviour improved
- the fan responded immediately and dramatically
- fan speed rose to approximately 5000 RPM
- CPU temperature began falling quickly
- Reese stopped operating near thermal limits
- the loud fan response confirmed that the cooling hardware was functional
- fan speed later settled around approximately 1900 RPM during normal operation
- no replacement fan was required

## Act V-A: Reese Attempts Vertical Takeoff

The moment macfanctld began actively managing the fan, the cooling hardware made its position clear. The fan accelerated with startling immediacy to approximately 5000 RPM, a response so sudden and theatrical that the Committee briefly considered whether the investigation had become an aviation matter.

### Flight Recorder

- Fan speed: Approximately 5000 RPM
- CPU temperature: Falling rapidly
- Fan hardware status: Extremely alive
- Chassis altitude: Unchanged
- Runway clearance: Not granted
- Committee composure: Reduced
- Root’s enthusiasm: Unhelpfully high

The increase in fan speed was immediate and dramatic, and the thermal response was equally swift. CPU temperature began falling quickly, which was the important technical result and also the most inconveniently exciting part of the incident. The loud fan response confirmed that the cooling hardware was functional. Later, after the initial dramatic burst, the fan settled into a normal operating speed of approximately 1900 RPM.

The absurd interpretations were many and, in the Committee’s opinion, entirely justified:

- Reese appeared to request runway clearance
- the aluminium chassis briefly became an aviation project
- loose paperwork within a reasonable radius was considered at risk
- Root declared the fan “extremely cooperative”
- Finch questioned whether Reese was cooling itself or attempting to leave the cupboard
- Fusco reported possible crosswind
- Bear prepared for an unexpected aerospace load
- the garage cupboard was temporarily redesignated as Launch Complex Reese
- the Committee checked whether the Mac mini had developed lift
- the fan’s defence lawyer submitted 5000 RPM as proof of innocence
- the cupboard denied issuing takeoff clearance
- nearby dust was evicted at operational velocity
- Health & Safety requested hearing protection and a flight plan
- Finance Department asked whether aviation insurance was now required

No physical movement occurred. No object was airborne. No hardware failed. No actual hearing protection was required. The only thing that left the scene was the Committee’s sense of proportion.

## Act VI: The Fan Is Cleared

The fan was treated as a wrongly accused suspect. It was:

- present
- physically functional
- capable of spinning
- waiting for proper management
- accused before being interviewed
- ultimately cleared of all charges

The cupboard was also formally cleared again.

> “The cupboard cooperated fully with investigators and was released without charge.”

## Systems Involved

- Reese
- 2012 Mac mini hardware
- Ubuntu Server
- CPU temperature sensors
- internal cooling fan
- macfanctld
- systemd
- environmental monitoring stack
- Arduino R3
- dual DS18B20 sensors
- Prometheus
- Grafana
- Reese Baking Index
- garage cupboard
- Committee suspect board
- Finch’s rapidly rising concern

## Technical Root Cause

The extreme CPU temperature was not caused by unsafe cupboard ambient conditions or a failed fan.

The root cause was that appropriate Apple-specific fan-control management was not active under Ubuntu Linux. The fan hardware remained functional, but without suitable active control it did not respond adequately to thermal conditions.

Installing and enabling macfanctld restored proper fan behaviour and reduced CPU temperatures.

## Actions Taken

1. Confirmed the CPU temperature was genuinely excessive.
2. Checked the surrounding cupboard temperature.
3. Reviewed CPU load and internal cooling behaviour.
4. Considered fan hardware failure.
5. Investigated Linux fan control on 2012 Mac mini hardware.
6. Identified macfanctld as the required management layer.
7. Installed and configured macfanctld.
8. Started and enabled the service.
9. Monitored temperature and fan response.
10. Confirmed a substantial temperature reduction.
11. Continued long-term observation through existing monitoring.
12. Formally cleared the cupboard and fan of wrongdoing.

## Validation

The following were verified as part of the operation:

- CPU temperatures fell significantly after macfanctld was activated
- fan speed responded appropriately
- normal fan speed later sat around approximately 1900 RPM
- Reese remained stable
- no replacement fan was required
- environmental sensors continued showing acceptable cupboard conditions
- the fix persisted under normal operation
- monitoring remained available in Grafana or related tools

## Outcome

- Reese was rescued from excessive CPU temperatures
- the fan was proven functional
- macfanctld was installed and enabled
- thermal behaviour became stable
- the cupboard remained innocent
- the environmental monitoring project was vindicated
- system-level temperature monitoring proved essential
- Finch avoided unnecessary hardware replacement
- Root obtained enough drama for one episode despite the rapid solution

## Mission Status

COMPLETED — THERMAL MANAGEMENT RESTORED

> The case remained open for long-term temperature observation, primarily because the Committee had already built the dashboards.

## Coffee Status

- High-temperature discovery: Coffee placed down abruptly
- Fan-failure hypothesis: Fresh cup authorised
- Suspect-board construction: Coffee forgotten
- macfanctld discovery: Coffee still too hot to drink
- Temperature recovery: Victory coffee
- Realisation the case was almost immediately solved: Mild resentment

## Casualties

- trust in default fan behaviour
- one innocent fan’s reputation
- several absurd hypotheses
- the assumption that healthy ambient temperature guarantees healthy CPU temperature
- Root’s planned multi-day investigation
- Finch’s belief that the fan had died
- several dust particles displaced without due process
- Root’s remaining ability to describe the event calmly
- the garage cupboard’s classification as a non-aviation facility
- no hardware
- no nearby objects
- no actual aircraft
- no actual casualties

## Lessons Learned

- ambient temperature and component temperature are different measurements
- monitor CPU temperature directly
- Linux on Apple hardware may require hardware-specific management tools
- confirm fan-control services are installed and running
- do not replace a fan before confirming the control layer
- verify services persist after reboot
- use logs and sensor data before opening hardware
- a functioning fan can still be functionally ineffective without proper control
- environmental monitoring did not fail; it measured a different layer of the problem
- high CPU temperature requires prompt investigation
- clearing the cupboard once does not prevent it being questioned again
- Root can construct a twelve-suspect case board before checking whether a service exists
- Ubuntu had adopted a passive management philosophy
- the fan was not dead; it was under-managed
- a Mac mini at 100°C is not “running warm”
- aluminium should not feel emotionally committed to becoming cookware
- every successful sensor project eventually discovers a different problem
- the Committee’s most elaborate thermal investigation was solved by installing a daemon
- the phrase “the cupboard is fine” requires scope clarification
- no one should say “it’s probably fine” while the CPU exceeds boiling-adjacent temperatures
- a fan reaching approximately 5000 RPM is compelling evidence that it is not dead
- sudden correct fan behaviour can be both reassuring and deeply theatrical
- verify the control layer before accusing the hardware
- thermal recovery may arrive with sound effects
- a Mac mini can create an unreasonable amount of aviation imagery without leaving the shelf

## Official Findings

The Committee concluded that the high CPU temperature was genuine, the cupboard environment remained within acceptable conditions, the fan hardware was functional, and fan control under Ubuntu was insufficient without macfanctld. macfanctld corrected the issue. The approximately 5000 RPM response provided immediate evidence that the fan hardware was functional. The dramatic increase in fan speed coincided with rapid thermal recovery. The fan later returned to a normal operating speed of approximately 1900 RPM. Temperature fell dramatically. No fan replacement was required. The environmental-monitoring project remained valid. The investigation generated far more narrative tension than technical complexity. Root’s suspect board was excessive but visually impressive. Finch was justified in being concerned. The fan is owed a formal apology.

## Committee Findings

### Finch

> “The temperatures are too high.”

### Root

> “Then we investigate everything with maximum enthusiasm and minimum evidence.”

### The Cupboard

> “I was already cleared.”

### The Fan

> “Nobody asked me to spin faster.”

### Finch

> “Why does Reese sound like it is preparing for takeoff?”

### Root

> “The fan is responding correctly.”

### The Fan

> “I would like the record to show that I was never dead.”

### Reese

> “Requesting clearance to leave the cupboard and continue this conversation elsewhere.”

### The Cupboard

> “Denied. This facility is not a runway.”

### Health & Safety

> “Remain grounded and do not make the situation more dramatic.”

### Ubuntu

> “I was waiting for explicit configuration.”

### Reese

> “I was getting slightly uncomfortable.”

### Health & Safety

> “The phrase ‘slightly uncomfortable’ is not acceptable for temperatures above 100°C.”

### Finance Department

> “Has a replacement fan already been purchased?”

### Root

> “No, but I was prepared to spend a great deal of money on emotional reassurance.”

## Official Suspect Disposition

### The Cupboard
Status: Cleared

Reason: Ambient conditions remained acceptable.

### The Fan
Status: Cleared with apology

Reason: Hardware was functional but lacked appropriate management.

### CPU Load
Status: Insufficient evidence of wrongdoing

Reason: No supported finding that workload alone caused the incident.

### Dust
Status: Questioned and released

Reason: No confirmed evidence that dust was the primary cause.

### Docker
Status: Dramatically accused, not charged

Reason: No rogue container was proven to have discovered fire.

### Ubuntu
Status: Cooperative witness

Reason: Operating correctly within the configuration provided, but requiring Apple-specific fan-control assistance.

### macfanctld
Status: Key witness and eventual hero

Reason: Restored active fan management.

### Root
Status: Investigator under review

Reason: Constructed an extensive conspiracy board before checking the obvious software layer.

## Final Verdict

### Reese was found:

- Not being baked by the cupboard
- Not suffering from a dead fan
- Not mining cryptocurrency without permission
- Not attempting atmospheric re-entry
- Not secretly becoming a sandwich press
- Running far too hot
- In need of proper fan management
- Stable after macfanctld

### The fan was found:

- Alive
- Functional
- Innocent
- Underemployed
- Waiting for instructions
- Unfairly accused
- Much more effective after management arrived

### Ubuntu was found:

- Stable
- Capable
- Calm
- Unaware of the Committee’s panic
- In need of Apple-specific assistance
- Technically doing exactly what had been configured
- Operating under a thermal-management philosophy best described as “vibes”

### Root was found:

- Correct to investigate
- Excessively enthusiastic
- In possession of an unnecessary suspect board
- Prepared to dismantle the crime scene
- Mildly disappointed by the speed of the solution
- Required to apologise to the fan

### The cupboard was found:

- Fine
- Still fine
- Exactly as fine as previously measured
- Deeply tired of being questioned
- Entitled to legal representation during future thermal incidents

### The 5000 RPM Event was found:

- Loud
- Immediate
- Thermally effective
- Aerodynamically unproductive
- Excellent evidence for the defence
- Unnecessary grounds for runway construction
- The most dramatic thirty seconds of the investigation

## Best Quote

> “The fan was fine. Ubuntu was just vibes.”

> “The cupboard is fine. Reese is not.”

## Follow-On Operations

- [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked)
- [Operation Environmental Reconnaissance](/Operations/Operation-is-Reese-being-slowly-baked)
- ongoing Grafana temperature monitoring
- monitoring fan RPM
- monitoring CPU and SSD temperature
- Saturday maintenance checks
- verifying macfanctld persistence after updates or reboot
- future Reese hardware replacement planning
- Operation Bring Root Inside The Machine, if relevant as a future project

## Series Status

Operation The Fan Was Fine, Ubuntu Was Just Vibes was commissioned as a slow-burn thermal crime drama. An enormous suspect board was built. Investigators expected hardware failure or environmental conspiracy. The case was solved almost immediately when they discovered the missing fan-control service. The network attempted to stretch the case into multiple episodes until Reese briefly reached approximately 5000 RPM and the planned slow-burn crime drama was reclassified as an aviation thriller. The reclassification was short-lived because the chassis remained stubbornly grounded. The fan demanded an apology and declined promotional interviews. The cupboard threatened legal action if named as a suspect again.

## Related Documentation

- [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked)
- [Monitoring Infrastructure](/Infrastructure/Monitoring)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Operation I Swear We Automated This](/Operations/Operation-i-swear-we-automated-this)
- [Operation Preventative Existential Crisis](/Operations/Operation-preventative-existential-crisis)
- [Operation Archive](/Operations/Operation-Archive)
- [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox)
- [Library Status](/Library-Status)
- [Canon](/Canon)
