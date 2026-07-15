---
title: Operation Copycat Deluge
description: Evaluation of Deluge as a potential future torrent client while preserving the existing rTorrent workflow.
published: true
date: 2026-07-15T04:47:41.902Z
tags: 
editor: markdown
dateCreated: 2026-06-11T06:43:33.070Z
---

# Operation Copycat Deluge

## Objective

Evaluate Deluge 2.2.0 as a potential future torrent client for the RapidSeedbox environment while preserving the existing rTorrent workflow and active torrent fleet.

The primary goal was to determine whether Deluge could support category-aware export automation, allowing completed torrents to continue seeding while media is exported for Syncthing distribution and Arr import workflows

---

## Background

The seedbox currently operates using rTorrent and ruTorrent, integrated with Sonarr and Radarr.

The existing environment is stable and supports an active fleet of approximately 109 torrents. Any testing needed to avoid disruption to the production workflow.

The investigation began as a reconnaissance exercise but evolved into the implementation of a working export automation proof-of-concept.

---

## Investigation Summary

### Environment

* RapidSeedbox VPS
* Deluge 2.2.0
* rTorrent / ruTorrent production environment
* Sonarr integration
* Radarr integration
* Syncthing export workflow

### Existing Categories

The existing automation environment uses:

* tv
* movies
* movies4k

These categories are supplied by Sonarr and Radarr and drive the current media management workflow.

---

## Findings

### Deluge Status

* Deluge already installed and operational.
* WebUI accessible and functional.
* Existing plugin support available.
* Suitable for isolated testing without affecting rTorrent.

### Execute Plugin Investigation

The Execute plugin was investigated and source code reviewed.

Confirmed trigger events:

* Torrent Added
* Torrent Complete
* Torrent Removed

Confirmed script arguments:

* `$1` = Torrent ID (hash)
* `$2` = Torrent Name
* `$3` = Download Location

A test script successfully verified argument passing and event execution.

### Label Investigation

The Label plugin was investigated to determine whether Arr categories could be used for automation.

Label data was confirmed to be stored within:

```text
~/.config/deluge/label.conf
```

Supported labels:

* tv
* movies
* movies4k

Hash-to-label mapping was successfully implemented.

---

## Export Automation Implementation

A production export script was developed:

```text
~/bin/deluge-export.sh
```

Workflow:

```text
Torrent Completes
        ↓
Execute Plugin Fires
        ↓
Torrent Hash Received
        ↓
Label Lookup Performed
        ↓
Destination Selected
        ↓
Media Copied To Export Folder
        ↓
Event Logged
```

Export destinations:

```text
/home/user/export/tv
/home/user/export/movies
/home/user/export/movies4k
```

Logging:

```text
/home/user/deluge-export.log
```

The script uses:

```bash
cp -an
```

to preserve file attributes and prevent accidental overwrites.

---

## First Successful Production Export

The first verified export was:

```text
The.Daily.Show.2026.05.21.Weird.Al.Yankovic.1080p.HEVC.x265-MeGusta
```

Successful log entry:

```text
tv |
/home/user/export/The.Daily.Show.2026.05.21.Weird.Al.Yankovic.1080p.HEVC.x265-MeGusta
->
/home/user/export/tv
```

This confirmed successful end-to-end operation.

---

## Final Architecture

```text
Deluge
   │
   ├── tv
   ├── movies
   └── movies4k
            │
            ▼
    deluge-export.sh
            │
            ▼
        export/
        ├── tv
        ├── movies
        └── movies4k
            │
            ▼
        Syncthing
            │
            ▼
        Sonarr/Radarr
```

---

## Decision

No migration of the existing rTorrent fleet was performed.

The production environment remains unchanged and fully operational.

Instead, Deluge was successfully configured as a parallel proof-of-concept environment capable of category-aware export automation.

This provides a future migration path while preserving the stability of the current platform.

---

## Outcome

The investigation exceeded its original objectives.

The project successfully:

* Documented Deluge capabilities.
* Reverse engineered Execute plugin behaviour.
* Confirmed label-based automation.
* Implemented category-aware export automation.
* Preserved the existing torrent fleet.
* Established a future migration path.

No active torrents were migrated.

No production services were disrupted.

No rollbacks were required.

---

## Status

Mission Complete

## Date

11 June 2026

---

## Damage Report

* Legacy Torrents Lost: 0
* Data Corruption Events: 0
* Rollbacks Required: 0
* Excrement Incidents: 0
* Hammer Injuries: 0

---

## Lessons Learned

* Deluge is more capable than initially expected.
* The Execute plugin provides powerful automation hooks.
* Category-aware export workflows are practical.
* Safe, conservative automation is preferable to aggressive automation.
* Understanding a replacement platform is valuable even when no migration occurs.
* Documentation often becomes as valuable as the technical outcome itself.

---

*"We set out to determine whether Deluge could replace rTorrent. The answer was yes. Unfortunately we discovered this by accidentally making Deluge useful."*
