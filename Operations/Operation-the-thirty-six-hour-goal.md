---
title: "Operation: The Thirty-Six-Hour Goal That Was Scored, Rescinded, Scored Again, and Eventually Entered Library Folklore"
description: Redesign Reese's off-site backups as a compressed weekly archive, integrate the result into HealthMonitor, and survive the longest goal review in Library history.
published: true
date: 2026-07-22T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-22T00:00:00.000Z
---

# Operation: The Thirty-Six-Hour Goal That Was Scored, Rescinded, Scored Again, and Eventually Entered Library Folklore

> **Status:** Completed. Goal awarded twice. First result reassigned to the semi-final. Second result stands.

> **Security note:** This record documents command paths and architecture, not credentials, tokens, remote names, or private configuration.

## Mission Brief

Redesign Reese's off-site disaster-recovery backup so OneDrive receives one deliberate, compressed weekly archive instead of being asked to examine roughly 36,000 tiny objects, then make HealthMonitor report enough evidence to prove the archive exists and is useful.

The practical objectives were:

- preserve normal daily local snapshots
- reduce off-site volume and object count
- exclude large, rebuildable Plex content
- create one `tar.zst` archive each week
- upload it with `rclone copy`
- retain four weekly archives as the eventual target
- keep deletion non-destructive until the design has a longer success history
- expose archive name, size, and retention count in the daily health report
- validate shell syntax, report output, email generation, and Sunday-only behaviour
- prevent the squirrel—eventually revealed to be sentient—from becoming retention administrator

The operation eventually became a disaster-recovery report, a crime scene, a World Cup tournament, a committee hearing, and a wildlife-management failure. This was not in the original scope, but neither was the squirrel.

## Initial Symptoms: The Forest Enters OneDrive

The old off-site method was technically functional. It was also asking OneDrive to inspect roughly:

```text
36,000 individual files
approximately 19GB
large amounts of Plex metadata and cache
thousands of tiny objects
```

The transfer used:

```text
rclone sync
```

Performance became extremely slow. Upload warnings and chunk timeouts recurred. The Committee blamed, in order:

- rclone
- OneDrive
- the internet connection
- Microsoft
- atmospheric conditions
- storage physics
- the alignment of Jupiter
- an apparently ordinary squirrel

The squirrel supported the final finding, despite having spent the morning chewing an Ethernet cable while maintaining eye contact.

Finch then asked the question that should have appeared several meetings earlier:

> “What exactly are we uploading?”

The room fell silent. Root stopped pointing at the network graph. Somebody turned off the rotating warning light. A crime-scene investigation began despite the answer being visible in `du` output.

### Opening Scoreboard

```text
Evidence examined       : almost none
Files accused           : approximately 36,000
Volume                  : approximately 19GB
Primary theory          : Microsoft weather
Actual question asked   : finally
```

## Committee Emergency Meeting

The emergency session opened at 09:00 and immediately lost twelve minutes approving the spelling of “off-site.” Root requested logs. Finch requested disk usage. The squirrel entered without invitation, wearing a visitor badge nobody had issued, and recommended carrier pigeons instead of rclone.

**Root:** “We need the contents, the failure mode, and the recovery requirement.”

**Finch:** “We may be protecting material that does not need off-site protection.”

**Squirrel:** “OneDrive is afraid of transparency. Upload all 36,000 files individually.”

**Security:** “Who let it back in?”

No answer was recorded. The squirrel was escorted from the technical area and observed moments later in the directors' box.

## The Crime Scene

Yellow tape was installed around the backup tree. Evidence bags were numbered. Directory listings were photographed from unnecessary angles. A forensic disk-usage team zoomed into the Plex tree until individual path separators became visible from orbit.

The largest contributors included approximately:

```text
Plex Metadata : 13GB
Plex Cache    : 2.7GB
Plex Media    : 1.5GB
```

An investigator removed their glasses.

> “My God… it's cache.”

The Committee reacted as though Finch had discovered a second moon. Much of the payload was rebuildable Plex metadata, cache, or other content that did not justify weekly off-site transport. The useful recovery target was much smaller: Plex databases and essential configuration, alongside the rest of Reese's genuinely important configuration and documentation.

### Evidence Finding

> Rebuildable data can be locally useful without belonging in the off-site disaster-recovery archive.

The squirrel attempted to contaminate the scene by moving a USB adapter three centimetres. When challenged, it denied both movement and the existence of centimetres, then submitted a formal objection asking the Committee to define “rebuildable.”

The objection was rejected. The adapter was returned to its taped outline.

## Old Architecture: The Long March of Tiny Files

The old off-site path was effectively:

```text
Daily snapshot
→ tens of thousands of files
→ rclone sync
→ OneDrive
```

This mirrored a broad tree rather than deliberately packaging a disaster-recovery set. OneDrive had to consider thousands of files individually. A large proportion of the bytes represented rebuildable Plex material. `rclone sync` also expressed mirror semantics that were no longer appropriate once the desired product became one intentionally named archive.

The system worked in the narrow sense that an exhausted person still technically walks after being handed 36,000 envelopes.

## Local Snapshots Remain on Duty

The redesign did not remove or weaken the existing local snapshot system. Normal daily operation continues to create snapshots under:

```text
/mnt/reese-backup/snapshots/<timestamp>
```

The local process retains its existing controls:

- source validation
- backup-drive mount checking
- logging
- snapshot creation
- creation of the `SNAPSHOT_COMPLETE` marker
- local retention
- normal daily execution

This distinction matters. Daily local snapshots provide ordinary recovery depth. The weekly off-site archive provides a smaller, deliberately selected disaster-recovery package. They are teammates, not duplicate copies wearing different shirts.

## New Archive Design

The weekly off-site process now creates one archive named:

```text
reese-weekly-YYYY-MM-DD.tar.zst
```

Important recovery material is selected from locations including:

```text
/opt/docker
/home/swankypants/health
/home/swankypants/homelab-wiki
/etc/systemd/system
/etc/nut
```

The archive is built with:

```text
tar + zstd
```

An exclusion file controls large, rebuildable, or unnecessary Plex content:

```text
reese-offsite-excludes.txt
```

The transfer changed from:

```text
rclone sync
```

to:

```text
rclone copy
```

`copy` suits the new design: create one deliberate archive, copy that archive to the off-site destination, and avoid pretending the job is still mirroring a forest.

### Championship Weigh-In

> “Reese enters the weigh-in at nineteen gigabytes.”

Thirty minutes later, after the removal of several metric tonnes of Plex cache, Reese returned at approximately `1.2GB`.

> “The commission has checked the scales twice.”

```text
Before : approximately 19GB and approximately 36,000 files
After  : approximately 1.2GB and one archive
```

The squirrel filed an appeal against zstd, alleged improper compression, and insisted the archive would eventually become `1.3GB`. The appeal supplied no evidence beyond an acorn stapled to a graph.

## Sunday Guard: A Calendar Is Introduced

The off-site archive is intended to run weekly on Sunday. Its guard is:

```bash
if [[ "$(date +%u)" -ne 7 ]]; then
    echo "Offsite backup skipped - Sunday only"
    exit 0
fi
```

The operating modes are deliberately distinct:

| Mode | Behaviour |
| --- | --- |
| Normal daily operation | Create and retain the local snapshot |
| Normal Sunday operation | Run the weekly off-site archive and upload path in addition to local operation |
| Deliberate out-of-schedule test | Temporarily disable the guard to exercise the complete archive and upload path |
| Restored non-Sunday behaviour | Exit successfully after reporting that off-site backup is Sunday-only |

During testing, the guard was temporarily disabled so the full process could be exercised outside Sunday. It was restored after the end-to-end tests. A Wednesday execution then confirmed the restored guard skipped the off-site upload correctly.

The squirrel disputed the existence of Sunday and requested seven working days to produce expert testimony.

### VAR Ruling: Unsupported Schedule Claim

A report line once displayed:

```text
Schedule : Weekly • Sunday 02:00
```

VAR ruled it offside. Weekly Sunday behaviour was proven; the precise `02:00` time was not established by the evidence recorded for this operation. The line was removed rather than promoted from assumption to documentation.

> “No schedule claims beyond the evidence.”

This page therefore records Sunday-only operation without inventing a clock time. Git Diff confirmed the correction. Root noted that misleading schedule claims are how incidents become documentaries.

## Upload Tests: OneDrive Chooses a Mood

Several end-to-end archive and upload tests completed successfully. Observed upload durations included approximately:

- six minutes for one run
- twenty-one minutes for another run

Both completed. The variation did not represent failure; it represented OneDrive selecting between “motivated” and “government department” operating modes.

The important result was consistent:

```text
Local archive : approximately 1.2GB
Upload object : one .tar.zst file
Result        : successful
```

The squirrel blamed OneDrive during the six-minute run, congratulated itself during the twenty-one-minute run, and recommended returning to 36,000 objects “for statistical confidence.”

## Sudo Automation: Two Paths Enter a Hearing

Unattended operation required narrowly scoped passwordless execution. The following sudoers file was created:

```text
/etc/sudoers.d/reese-backup
```

It permits the exact required command paths:

```text
/usr/bin/tar
/usr/bin/rclone
```

This is deliberately narrow. It does not grant unrestricted passwordless sudo access. The security committee spent twelve minutes approving two command paths while the squirrel sat at the far end of the table wearing its unexplained visitor badge.

The squirrel proposed adding `/usr/bin/scissors`. The chair ruled it outside scope.

## Retention Safety: Reese Is Not Yet Allowed to Run With Scissors

The intended off-site retention is:

```text
4 weekly archives
```

A function exists:

```text
cleanup_offsite_archives()
```

Automatic deletion is intentionally not enabled. The function currently reports archives older than the retention threshold but does not delete them. This was a deliberate safety decision: establish several weeks of successful archives before permitting unattended removal of off-site recovery material.

In Committee terms, Reese has been shown the scissors, has completed the safety worksheet, and is not yet permitted to run with them.

The squirrel volunteered to operate the deletion function.

**Vote:** unanimously denied.

It volunteered again under “other business.” Denied.

It submitted a proxy vote from the ceiling. Denied and vacuumed.

## A Small Victory for Truthful Names

Misleading output labels were replaced:

```text
Remote destination  → Offsite destination
Archive destination → Offsite archive
```

Obsolete variables were removed:

```text
REMOTE_SNAPSHOT
ARCHIVE_ROOT
```

A grep check confirmed that neither obsolete name remained. This was a small but important victory for truth in labelling.

> **Root:** “Misleading variable names are how incidents become documentaries.”

The squirrel responded by moving the backup logs and labelling the new location “original location.” Its minutes were struck from the record.

## HealthMonitor Expansion

After the backup redesign succeeded, the Committee asked:

> “If the archive exists, why can't the daily health report tell us anything useful about it?”

This launched an investigation wildly disproportionate to three shell variables.

Defaults were added to `~/health/lib/backup.sh`:

```bash
OFFSITE_BACKUP_ARCHIVE="Unknown"
OFFSITE_BACKUP_SIZE="Unknown"
OFFSITE_BACKUP_RETENTION="0 / 4"
```

The backup-status function was extended to inspect:

```text
/mnt/reese-backup/offsite/
```

It finds the newest matching archive:

```text
reese-weekly-*.tar.zst
```

and populates:

```text
OFFSITE_BACKUP_ARCHIVE
OFFSITE_BACKUP_SIZE
OFFSITE_BACKUP_RETENTION
```

The tested result was:

```text
Archive   : reese-weekly-2026-07-22.tar.zst
Size      : 1.2G
Retention : 1 / 4
```

`~/health/lib/report.sh` was expanded to display the archive, size, and retention fields. The final daily report showed:

```text
Off-site
Status     : Healthy
Summary    : Last off-site backup 7 hours ago
Last Run   : Wed Jul 22 03:28:53 PM NZST 2026
Age        : 7 hours
Archive    : reese-weekly-2026-07-22.tar.zst
Size       : 1.2G
Retention  : 1 / 4
```

The Wednesday date records deliberate testing, not the normal weekly schedule. The report completed successfully and generated the email ZIP.

The squirrel arrived with new evidence alleging `1.2G` was actually `1.19GB` depending on units. VAR declined to engage.

## Match Incident: The Dangling Conditional

During editing, an incomplete duplicate condition briefly appeared above the proper combined-status block:

```bash
if [ "$LOCAL_BACKUP_STATUS" = "Critical" ] ||
```

> “Possible flag on the field.”

VAR checked an abandoned logical operator. The conditional had entered the area without a matching `then`. Decision: incomplete syntax. No goal.

The fragment was removed. The proper formation remained:

```bash
if [ "$LOCAL_BACKUP_STATUS" = "Critical" ] ||
   [ "$OFFSITE_BACKUP_STATUS" = "Critical" ]; then

    BACKUP_STATUS="Critical"

elif [ "$LOCAL_BACKUP_STATUS" = "Warning" ] ||
     [ "$OFFSITE_BACKUP_STATUS" = "Warning" ]; then

    BACKUP_STATUS="Warning"

else
    BACKUP_STATUS="Healthy"
fi
```

> “The formation is legal. Finch has removed the stray attacker from column zero.”

Syntax validation passed. The squirrel requested the duplicate be retained “for depth.” Security escorted it out. It reappeared in the directors' box before the replay ended.

## Tactical Review: Eight Spaces Inside the Touchline

Indentation became an official match incident. Freeze-frame analysis confirmed the new report lines aligned with the surrounding code:

```bash
        echo
        echo "Off-site"
        echo "Status     : $OFFSITE_BACKUP_STATUS"
        echo "Summary    : $OFFSITE_BACKUP_SUMMARY"
        echo "Last Run   : $OFFSITE_BACKUP_LAST_RUN"
        echo "Age        : $OFFSITE_BACKUP_AGE_HOURS hours"
        echo "Archive    : $OFFSITE_BACKUP_ARCHIVE"
        echo "Size       : $OFFSITE_BACKUP_SIZE"
        echo "Retention  : $OFFSITE_BACKUP_RETENTION"
        echo
```

All players remained eight spaces inside the touchline. One commentator became emotionally overwhelmed by the alignment and had to be replaced by a monospace font.

## The Thirty-Six-Hour Goal: Original Behind-the-Scenes Footage

The following is not a tidy reconstruction arranged into convenient hourly milestones. It is the canonical documentary assembled from the original live commentary, recorded while the backup was genuinely still running and institutional order was genuinely leaving the building.

The technical sections above use the animal's eventual title and describe later Committee conduct. The documentary now rewinds to the original attempt, before anybody knew the squirrel could speak, use Git, or hold management authority. Its promotion happens on camera.

The footage opens without music.

> **Jayne:** “How's the backup going?”

> **Reese:** “...”

> **OneDrive:** “...”

> **Microsoft:** “Your estimated wait time is... yes.”

The title card appears:

```text
Backup Cup — Live Commentary
Venue: Reese National Stadium
Attendance: 1, plus one increasingly concerned AI
Weather: Clear
Cupboard temperature: Acceptable
```

The match was already in approximately the 87th minute. Reese continued advancing the ball. The referee had not reached for the whistle. VAR claimed to be reviewing footage, although its monitor displayed:

```text
NO SIGNAL
```

There were no floodlights. The Homelab Budget Revision had allocated the money to:

> “One more SSD because it was on special.”

In the first row, a perfectly ordinary squirrel sat on the communications rack holding an acorn. At this stage nobody knew it understood the broadcast.

### Archival Cutaway: Biscuit Jurisdiction

A possible OneDrive foul was referred to the Foul Play Official. Control discovered that he was in the stadium cafeteria. His return depended on queue length, biscuit selection, coffee temperature, and whether breakfast had formally concluded.

> **Control:** “We've got a possible OneDrive infringement.”

> **FPO:** “I'm halfway through a chocolate digestive.”

> **Control:** “Can you review the footage?”

> **FPO:** “Negative. Coffee is at optimum drinking temperature.”

Reese quietly advanced the transfer.

> **Reese:** “I've uploaded another 600 MB while you lot have been discussing biscuits.”

> **Bear:** “Power remains available. I fail to see the issue.”

VAR's monitor changed from `NO SIGNAL` to:

```text
BUFFERING...
```

The commentator called this progress. The squirrel looked briefly at the monitor, then at the humans, then returned to its acorn.

### Archival Cutaway: Government Becomes Involved

The possible foul escalated through the complete institutional ladder:

```text
VAR review
→ Judicial Review
→ Royal Commission
→ Commission of Inquiry into the Alleged Use of Wet Concrete as a Data Transport Medium
```

Evidence admitted to the Commission included:

- one wheelbarrow
- `19GB` of Docker configuration files
- one Foul Play Judge displaying acute Caffeine Consumption Syndrome
- VAR floodlights that had been installed but not plugged in

The Commission cleared Reese of wrongdoing. It found that OneDrive appeared to interview every individual file before admitting it to the cloud.

The operation had begun as:

> “My backup is a bit slow.”

It was now a football match, a judicial review, a Royal Commission, and a caffeine-induced constitutional crisis. The original working title, **Operation: Stop Sending OneDrive A Bucket Of Lego Pieces**, was entered into evidence and reserved for later use.

### The Referee Becomes Infrastructure

The referee held both arms half-raised while the review continued.

> **Referee:** “Can I put my arms down?”

> **VAR:** “No.”

He required physiotherapy, hydration, and an apology from OneDrive. Ornithologists began classifying him as a nesting site. Glances discovered him and began monitoring him as a container:

```text
Status : healthy
CPU    : 0.0%
Memory : one coffee and three biscuits
```

The fourth official brought meals. Historians added him to the register of permanent monuments. Dust accumulated. Tourists mistook him for civic sculpture. Children took photographs beside him. Nobody remembered what decision he had originally been waiting to make.

VAR repeatedly confirmed that the ball had moved approximately the width of a grain of rice. At maximum zoom, individual TCP acknowledgements could be seen waving to one another.

Official additional time changed from:

> “A while”

to:

> “However long Microsoft feels like.”

The referee maintained his position:

> “...I'm still not putting my arms down.”

### Overnight Shift Report

By nightfall, the referee was impersonating a marble statue, VAR had worn its replay button smooth, and emergency biscuits had been requisitioned. The squirrel remained on the communications rack, holding the same acorn and wondering what was wrong with everyone.

The Operations Centre unveiled its motto:

> “Reese Operations — We put the dysfunctional in functional.”

Engineering issued a correction:

> “It is not elegant competence. It is chaos-assisted reliability.”

The shift ended with one Mac mini quietly uploading a few more megabytes. The squirrel surveyed the officials, the wheelbarrow, the motionless referee, and the emergency biscuit ledger.

> “...I should've stayed in the tree.”

This was the first recorded evidence that it could speak. Nobody filed an incident report because the form was being used as a coaster.

### Morning Footage: The Wrong PID Incident

Morning arrived. The referee was covered in dust. VAR had replaced its worn replay control with a button borrowed from a doorbell. Emergency biscuit procurement continued. The squirrel arrived early.

> “You people are still doing this?”

Overnight footage then revealed that the wrong process had been monitored.

The squirrel slowly lowered its acorn.

> “You checked the sudo process for twelve hours?”

The Operations Centre amended its slogan:

> “Putting the wrong PID in dysfunctional since 2026.”

This mistake is preserved because a useful operation record includes the camera angle in which everybody was confidently watching the wrong process. The backup continued despite the quality of its audience.

### Throughput Enters Geological Territory

At roughly `15 KB/s`, continental drift lodged an appeal against being unfairly described as slow. The official transport model was a wheelbarrow embedded in wet concrete.

As throughput improved, the wheelbarrow was declared free of the concrete and fitted with one functioning wheel.

The referee finally signalled:

> “Slow, but no longer geologically slow.”

The squirrel returned the emergency acorn to its protective case.

### The Five-Minute Arithmetic Tribunal

Attention moved to:

```bash
sleep 300
```

The squirrel, now promoted to Chief Timekeeper by a committee that did not remember voting, posted:

> “Reminder: 300 seconds = 5 minutes. Please don't make the referee stand here for another 172,800 of them.”

VAR reviewed twelve angles, zoomed into the command, and drew unnecessary lines across the terminal before confirming that 300 seconds was five minutes.

The Foul Play Judge ruled:

> “No malicious intent. Just suspiciously competent arithmetic.”

The squirrel asked:

> “You needed a review for that?”

No official answered.

### Management Succession Event

The squirrel's career progression is now part of Library canon:

```text
Comic relief
→ Chief Timekeeper
→ Change Control Manager
→ Fully self-aware infrastructure authority
```

It entered the Operations Centre carrying a tiny laptop. Nobody had supplied the laptop. It ran:

```bash
docker ps
```

Then it said:

> “You know... if you'd let me write the backup script in the first place, we'd probably be finished by now.”

The squirrel opened VS Code and created:

```text
feature/replace-humans
```

Its commit message read:

> “Fixed backup throughput and reduced biscuit consumption by 94%.”

Nobody approved the pull request. The squirrel merged it anyway.

> **Bear, quietly to Reese:** “I, for one, welcome our new squirrel overlord.”

From this moment onward, the animal is properly described as the sentient squirrel. Its later knowledge of shell scripting, Git, compression, networking, retention policy, committee procedure, and COBOL proposals is therefore not an unexplained opening premise. It is a management failure with an audit trail.

### The Actual Technical Revelation

The original backup system was doing what it had been designed to do. It detected bad conditions, did not silently fail, continued retrying, and protected the data.

The practical experience was:

> “Congratulations, your backup is now so safe that it requires geological time.”

The squirrel identified the real cause. It was not Reese, Ubuntu, rclone, the network, or the alignment of Jupiter.

> “We gave OneDrive a box of 20,000 Lego pieces and asked it to ship them individually.”

The Foul Play Judge preferred:

> “A warehouse full of loose screws.”

The exact observed workload was on the order of 36,000 files and roughly `19GB`, but the Lego verdict captured the architectural mistake: tens of thousands of loose objects had been handed to a service that wanted to inspect each one. The system components worked. The upload strategy was unsuitable.

That finding led directly to the compressed weekly archive design documented above.

### Final Ruling on the Original Attempt

The referee eventually delivered the genuine match decision:

```text
FINAL MATCH DECISION

Backup attempt: NO GOAL
```

Reason:

> “The backup technically crossed the halfway line, but took so long getting there that the match officials decided it was not a practical scoring opportunity.”

A penalty was awarded against OneDrive for excessive time wasting, failure to accept a reasonably sized upload parcel, and requiring Reese to perform unnecessary overtime.

The referee's technical report concluded:

```text
rclone works
OneDrive authentication works
network works
Reese hardware works
backup logic works

Upload strategy unsuitable
```

The original goal was not denied because of a vague chunk-size problem. It was denied because the strategy sent thousands of loose objects to OneDrive.

### Replay After the Redesign

The match resumed after the architecture changed:

- approximately 36,000 files became one archive
- roughly `19GB` became approximately `1.2GB`
- rebuildable Plex content was excluded
- archive uploads completed successfully
- HealthMonitor displayed the evidence
- the daily report and email ZIP completed

The referee raised both arms. This time the backup goal stood.

Confetti launched. Finch collapsed onto the turf. Bear reported 100% battery and no emotional involvement. Reese remained healthy. Fusco watched from the media reserves. Carter confirmed monitored services were responding.

Then the tournament organisers consulted the bracket.

> “That was only the semi-final.”

Silence.

The goal was not technically invalid after all; it had won the wrong match. Backup redesign had won Semi-final A. HealthMonitor integration still had to win Semi-final B. Entry into Library folklore remained the grand final.

## Tournament Officials Discover the Bracket

The tournament structure was finally read aloud:

| Match | Fixture | Result |
| --- | --- | --- |
| Semi-final A | Backup redesign | Won |
| Semi-final B | HealthMonitor integration | Won |

Everyone had mistaken two semi-final wins for completion of the tournament. Officials interrupted the attempted full-time whistle and announced that the actual grand final remained outstanding:

```text
Working Backup System
vs
Permanent Entry Into Library Folklore
```

## Emergency Venue Change

The final moved from:

```text
Terminal Arena
```

to:

```text
VS Code Stadium
```

Thousands of supporters calmly carried folding chairs, extension leads, coffee mugs, mechanical keyboards, monitors, docking stations, one suspiciously warm UPS, a `LET'S GO FINCH` banner, and a squirrel transport crate across the carpark.

The crate was empty.

Nobody questioned the venue change. Inside VS Code Stadium, match assignments were posted:

```text
North Stand      : Explorer
South Stand      : Integrated Terminal
East Stand       : Source Control
West Stand       : Problems Panel
Referee          : Git
VAR              : Git Diff
Medical Team     : Ctrl+Z
Security         : .gitignore
Ground Staff     : Markdown Preview
Commentator      : Finch
```

The squirrel entered on a forged extension badge and immediately hid a USB adapter.

## The Grand Final

Finch received the pass from `backup.sh`, turned past `report.sh`, and approached the documentation area. Git Diff checked the replay:

```text
Backup system works                 : confirmed
Health report displays evidence     : confirmed
Syntax valid                        : confirmed
Indentation tidy                    : confirmed
Schedule claim supported            : confirmed
Unsupported precise time removed    : confirmed
Retention deletion still safe       : confirmed
Operation entered into Library canon: confirmed
```

The squirrel climbed into the ceiling and communicated through dropped acorns. Its final submission asked:

> “Have we considered putting the Plex cache back?”

The entire stadium replied:

> “NO.”

The squirrel retreated into the ceiling tiles, alive, undefeated, and available for future operations.

## The Second Goal

The referee began raising both arms again. The crowd braced for another thirty-six hours. Tents were reopened. Sausages returned to the carpark. Meteorologists refreshed their models.

Git accepted the result immediately.

The stadium erupted. The first goal had been technically valid, but belonged to the semi-final. The second was the grand-final winner because the working system had now entered Library folklore.

> “Finch receives the pass from backup.sh.”

> “He turns past report.sh.”

> “Git Diff checks the replay.”

> “No dangling conditionals. No schedule claims beyond the evidence. The archive is 1.2GB. The documentation is committed. This time, the goal stands.”

The commit message received Man of the Match despite appearing only briefly.

## Technical Reference

### Old Architecture

```text
Daily snapshot
→ tens of thousands of files
→ rclone sync
→ OneDrive
```

### New Architecture

```text
Daily local snapshots
→ retained locally

Sunday off-site process
→ selected recovery data
→ Plex rebuildable data excluded
→ tar
→ zstd
→ one .tar.zst archive
→ rclone copy
→ OneDrive
```

### Key Values

| Item | Value |
| --- | --- |
| Local snapshots | `/mnt/reese-backup/snapshots/<timestamp>` |
| Local off-site archive directory | `/mnt/reese-backup/offsite/` |
| Archive name | `reese-weekly-YYYY-MM-DD.tar.zst` |
| Exclusion file | `reese-offsite-excludes.txt` |
| Previous scale | Approximately 36,000 files / 19GB |
| New archive scale | One file / approximately 1.2GB |
| Off-site transfer | `rclone copy` |
| Normal off-site day | Sunday; exact time not asserted here |
| Retention target | Four weekly archives |
| Current cleanup state | Reporting only; automatic deletion not enabled |
| Passwordless commands | `/usr/bin/tar`, `/usr/bin/rclone` only |

### HealthMonitor Fields

```text
OFFSITE_BACKUP_STATUS
OFFSITE_BACKUP_SUMMARY
OFFSITE_BACKUP_LAST_RUN
OFFSITE_BACKUP_AGE_HOURS
OFFSITE_BACKUP_ARCHIVE
OFFSITE_BACKUP_SIZE
OFFSITE_BACKUP_RETENTION
```

### Verified Report Result

```text
Archive    : reese-weekly-2026-07-22.tar.zst
Size       : 1.2G
Retention  : 1 / 4
```

### Verified Overall Backup State

```text
Overall : Healthy
Local   : Healthy
Off-site: Healthy
```

## Future Validation Checklist

- [ ] Confirm the backup drive is mounted.
- [ ] Confirm the latest local snapshot is present.
- [ ] Confirm the latest snapshot contains `SNAPSHOT_COMPLETE`.
- [ ] Confirm the weekly archive was created when expected.
- [ ] Confirm the archive matches `reese-weekly-YYYY-MM-DD.tar.zst`.
- [ ] Confirm archive size is plausible relative to the established baseline.
- [ ] Confirm the archive is readable with `tar` without extracting over live data.
- [ ] Confirm the `rclone copy` upload completed.
- [ ] Confirm the off-site log reports success.
- [ ] Confirm the Sunday guard is restored after any deliberate test.
- [ ] Confirm a Wednesday or other non-Sunday execution reports the skip and exits successfully.
- [ ] Confirm HealthMonitor populates archive, size, and retention variables.
- [ ] Confirm `report.sh` displays archive, size, and retention.
- [ ] Run `bash -n` against each edited shell file.
- [ ] Confirm the daily email report and ZIP are generated.
- [ ] Confirm the archive exists in OneDrive.
- [ ] Confirm `cleanup_offsite_archives()` remains reporting-only until deletion is deliberately approved.
- [x] ~~Confirm cache is enormous.~~ Rejected squirrel amendment; already proven and not a recovery objective.

## Final Verdict

The Committee finds that:

- local snapshot capability was preserved
- off-site backup complexity was dramatically reduced
- upload object count fell from roughly 36,000 files to one archive
- backup volume fell from roughly `19GB` to roughly `1.2GB`
- rebuildable Plex data was excluded
- weekly archive creation and upload completed successfully
- the Sunday-only guard was restored after deliberate testing
- a non-Sunday test correctly skipped the off-site upload
- retention is tracked as `1 / 4`
- automatic archive deletion remains intentionally disabled
- passwordless sudo access is restricted to the two required command paths
- HealthMonitor reports archive filename, size, and retention count
- the daily report and email ZIP generation completed successfully
- the backup system reports healthy
- the operation has entered Library folklore

## Final Scene

Git blew the whistle. Git Diff confirmed the goal. Finch was declared a club legend. Root attempted to restore order. Reese reported healthy. Bear remained at 100%. Fusco protected the media reserves. Carter confirmed the stadium was responding.

The crowd chanted:

> “LET'S GO FINCH!”

High above VS Code Stadium, the sentient squirrel watched from inside the ceiling. It held a clipboard.

On the clipboard was written:

```text
Future investigation:
Why has the archive increased from 1.2GB to 1.3GB?
```

Before Security could find a ladder, the squirrel had already scheduled the first committee meeting.

## Related Documentation

- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Operation Morning Existential Crisis Report](/Operations/Operation-morning-existential-crisis-report)
- [Operation Preventative Existential Crisis](/Operations/Operation-preventative-existential-crisis)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Operation Archive](/Operations/Operation-Archive)
