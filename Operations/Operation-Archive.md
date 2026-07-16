---
title: Operation Archive
description: Central register of documented, recovered, planned, and possibly fabricated homelab operations.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Operation Archive

The Operation Archive is the central register of missions undertaken, proposed, remembered, or confidently mentioned by somebody who then failed to write the page.

> **Archive note:** Some entries were recovered from memory and old chat fragments. Treat them as leads until properly filed.

Newly recovered fragments belong in the [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox). When enough evidence exists to create a dedicated record, start with the [Operation Template](/Operations/Templates/Operation-Template).

Statuses describe the evidence currently held by The Library, not necessarily the state of every underlying service. Where the archive knows only a name, it says so. Root has been asked not to improvise the missing incident report.

## Documented Operations

These operations have a dedicated page or case file containing useful evidence.

| Operation | Status | System / Area | Summary | Needs Page? |
|---|---|---|---|---|
| [Operation Copycat Deluge](/Seedbox/Operation-Copycat-Deluge) | Active / documented | Seedbox and media acquisition | Evaluates Deluge alongside the existing rTorrent workflow and tests category-aware export automation. | No |
| [Operation Is Reese Being Slowly Baked?](/Operations/Operation-is-Reese-being-slowly-baked) | Completed; monitoring continues | Reese and cupboard environment | Investigated Reese's thermal conditions and established ongoing environmental monitoring. | No |
| [Operation Spinny Rust Prison Break](/Operations/Operation-spinny-rust-prison-break) | Completed | Reese storage and migration | Retired Reese's old spinning disk and enabled the SSD-era migration work that followed. | No |
| [Operation Build The Library](/Operations/Build-the-library) | Completed | The Library | Established Wiki.js and PostgreSQL on Reese as the homelab documentation system. | No |
| [Operation Electrons Are A Privilege, Not A Right](/Operations/Operation-electrons-are-a-privilege-not-a-right) | Completed | Bear and power monitoring | Connected Bear to Reese through NUT and integrated UPS health with Prometheus, Grafana, HealthMonitor, and ntfy. | No |
| [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report) | Completed | HealthMonitor and daily reporting | Created the automated daily homelab health report, corrected its cron path, and added ZIP retention, email, and ntfy delivery. | No |
| [Operation Creepy Van Network](/Operations/Operation-creepy-van-network) | Completed; follow-up planned | Tailscale and remote access | Established secure tailnet access and MagicDNS without public exposure; VPN-on-Demand testing and broader friendly-name integration remain planned. | No |
| [Operation Fusco, Open The Damn Door](/Operations/Operation-fusco-open-the-damn-door) | Completed | Fusco storage and SMB mounts | Configured reliable CIFS mounts on Reese so Plex, the Arr stack, backups, and other services could use consistent storage paths. | No |
| [Operation Copycat: The Whitespace Assassin & The Rain Dance Tunnel](/Case-files/Whitespace) | Resolved case file | Seedbox automation | Investigated whitespace and script behaviour encountered during Operation Copycat Deluge. | No |

## Recovered From Memory

These names survive in overview pages, Ancient Texts, or operation references, but their dedicated records have not yet been recovered.

| Operation | Status | System / Area | Summary | Needs Page? |
|---|---|---|---|---|
| Operation SSD Rebirth | Completed / recovered name | Reese storage | Follow-on work enabled by Spinny Rust Prison Break; the surviving name indicates Reese's SSD transition. | Yes |
| Operation Get In Loser, We're Migrating | Completed / recovered name | Reese migration | Historical migration operation referenced by Reese's overview and the storage operation legacy. | Yes |
| Operation One Does Not Simply Move Plex | Completed / recovered name | Plex migration | Historical Plex migration whose title correctly suggests paths, databases, and consequences were involved. | Yes |

## Referenced But Not Yet Filed

These operations have useful context elsewhere in The Library but still deserve their own page.

| Operation | Status | System / Area | Summary | Needs Page? |
|---|---|---|---|---|
| Operation Environmental Reconnaissance | Active / ongoing observation | Reese and cupboard environment | Follow-on to the baking investigation for seasonal trends, alerting, and possible cooling decisions. | Yes |

## Future Operations

These are candidates from the Future Projects desk. Finch has not necessarily signed the paperwork, and operation names may still be pending.

| Operation | Status | System / Area | Summary | Needs Page? |
|---|---|---|---|---|
| Future Plex Migration | Proposed | Plex and media services | Plan the next Plex migration before any service or path is moved. | Yes, when approved |
| Smart Cupboard Cooling | Proposed | Reese and cupboard environment | Investigate cooling or airflow automation using collected environmental evidence. | Yes, when approved |
| Local AI Expansion | Proposed | Local compute and assistance | Evaluate additional local AI capability without pretending Reese has infinite resources. | Yes, when approved |
| Additional Monitoring | Proposed | Monitoring | Extend useful coverage where a clear signal, response, and owner exist. More graphs alone do not constitute preparedness. | Yes, when approved |

## Possible Committee Fabrications

These names currently exist as title cards inside practical runbooks. They are valid canon-adjacent labels, but there is no evidence that Finch opened a formal operation file.

| Operation | Status | System / Area | Summary | Needs Page? |
|---|---|---|---|---|
| [Operation Preventative Existential Crisis](/Operations/Saturday-Maintenance-Runbook) | Recurring runbook title | Weekly maintenance | Saturday checks intended to find problems before they become Tuesday night incidents. | No; use the runbook |
| [Operation Aluminium Crab Down](/Operations/Disaster-Recovery-Reese-Dies) | Emergency runbook title | Reese disaster recovery | Recovery plan for rebuilding Reese from backup on replacement hardware. | No; use the runbook |

---

If an operation gains real work, evidence, or consequences, give it a page and move it to the correct section. If it gains only a better joke, the Committee will hear the proposal after lunch.
