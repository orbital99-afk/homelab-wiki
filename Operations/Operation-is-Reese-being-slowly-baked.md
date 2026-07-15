---
title: Operation Is Reese Being Slowly Baked?
description: Environmental monitoring project to determine whether Reese was being slowly cooked inside a cupboard.
published: true
date: 2026-07-15T05:35:28.235Z
tags: 
editor: markdown
dateCreated: 2026-06-11T11:22:55.266Z
---

# Operation Is Reese Being Slowly Baked?

## Objective

Determine whether Reese was operating within safe environmental conditions while installed inside a cupboard.

The operation sought to answer a critical engineering question:

> Is Reese being slowly baked?

---

## Background

Following deployment of Reese as the primary homelab server, concerns were raised regarding long-term temperatures inside the cupboard housing the system.

While CPU temperatures appeared healthy, no environmental monitoring existed to measure the actual conditions surrounding the server.

The Committee therefore authorized a formal investigation.

---

## Phase 1: Sensor Development

A dual-sensor monitoring system was designed and built using an Arduino R3.

### Sensors

- Cupboard Temperature Sensor
- Room Temperature Sensor

The sensors continuously measure:

- Internal cupboard temperature
- External room temperature
- Temperature delta between the two

---

## Phase 2: Data Collection

Custom exporters were developed to expose temperature data to Prometheus.

Metrics collected:

- Cupboard Temperature
- Room Temperature
- Temperature Difference

Additional system metrics were combined with environmental data:

- CPU Temperature
- SSD Temperature
- Fan RPM

---

## Phase 3: Visualization

A dedicated Grafana dashboard was created.

The dashboard provides real-time visibility into:

- Environmental conditions
- Internal system temperatures
- Temperature trends
- Seasonal behaviour

The temperature delta became known as the:

**Reese Baking Index**

---

## Hardware

### Monitoring Platform

- Arduino R3

### Enclosure

- Cupboard Climate Control Interface

### Sensors

- Dual DS18B20 Temperature Sensors

---

## Notable Findings

### Cupboard Conditions

Testing demonstrated that cupboard temperatures remained stable and well within acceptable operating limits.

### Door Events

Environmental monitoring proved sufficiently sensitive to detect:

- Cupboard door openings
- Garage door activity
- Rapid air temperature changes

The resulting temperature graphs effectively functioned as a flight recorder for the cupboard.

---

## Outcome

No evidence was found that Reese was being slowly baked.

System temperatures remained healthy throughout the investigation.

The operation was therefore considered successful.

---

## Mission Status

COMPLETED

### Conclusion

Reese is not being slowly baked.

Further observation remains ongoing for seasonal analysis.

---

## Follow-On Operations

### Operation Environmental Reconnaissance

Established to provide long-term environmental monitoring and baseline collection.

Future objectives include:

- Seasonal temperature analysis
- Trend detection
- Environmental alerting
- Potential automated cooling solutions

---

## Lessons Learned

- Environmental monitoring is a completely reasonable response to wondering if a server is warm.
- Building custom sensors is significantly more entertaining than buying commercial ones.
- Temperature graphs become much more interesting when they are treated as evidence in an active investigation.
- A surprising amount of engineering effort can be justified by curiosity.
- Once a metric exists, it immediately becomes important.
- The phrase "Reese Baking Index" should never have become official terminology.
- The Committee will absolutely continue monitoring despite already knowing the answer.

---

## Official Findings

After extensive monitoring, data collection, dashboard creation, exporter development, sensor calibration, cable management, committee review, and several entirely scientific observations involving opening and closing doors:

**No evidence was found that Reese was being slowly baked.**

The Committee acknowledges this outcome was deeply disappointing from a dramatic storytelling perspective.

---

## Committee Findings

### Root

> "We built an environmental monitoring platform, custom exporters, Grafana dashboards, and a dedicated climate control interface."

### Finch

> "What did we learn?"

### Root

> "The cupboard is fine."

### Fusco

> "You did all that to discover the cupboard is fine?"

### Root

> "We now know *exactly how fine* it is."

### Health & Safety

> "Approved."

### Finance Department

> "Denied."

---

## Final Verdict

Reese was found:

- Not baked
- Not roasting
- Not simmering
- Not gently poaching
- Not being prepared sous-vide

Reese was merely existing within manufacturer-recommended operating temperatures.

---

*"Operation Is Reese Being Slowly Baked? was cancelled after one season when investigators discovered the answer was 'No'. The spin-off series, Operation Environmental Reconnaissance, has been renewed for additional seasons."*
