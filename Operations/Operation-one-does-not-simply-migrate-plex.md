---
title: Operation One Does Not Simply Migrate Plex
description: Document the migration of Plex from Fusco to Reese, including preparation, validation, and the surprisingly successful outcome.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation One Does Not Simply Migrate Plex

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Objective

Move Plex from Fusco, the Synology NAS, to Reese, the Ubuntu Mac mini, without losing:

- metadata
- watch history
- libraries
- posters
- settings
- users
- paths
- playback
- dignity

The central question was simple and terrifying:

> “Can Plex be moved without destroying everything?”

## Background

For a time, Plex had lived on Fusco. That arrangement had worked. The media storage host remained Fusco, and the application host had been the NAS. But Reese was becoming the primary homelab application host, and the architectural logic of moving Plex to Reese was obvious.

The Committee, however, treated the idea as though it involved a royal succession, a cursed relic, and at least one missing database. Plex was too important to migrate casually. It was too important to migrate without contingency plans. It was too important to migrate without at least one dramatic announcement and a very serious briefing.

The phrase “one does not simply migrate Plex” therefore became the official warning, and everyone agreed that the operation would be either a triumph of preparation or a cautionary tale involving broken libraries, suspicious paths, and a very public outage.

## Act I: The Proposal

The proposal came in the form of a practical question: could Plex be moved from Fusco to Reese while preserving the libraries and playback experience?

The reaction was immediate and theatrical. Everyone imagined the usual failure modes:

- metadata loss
- watch-history loss
- broken libraries
- incorrect paths
- permission crimes
- unavailable Fusco mounts
- users asking why Plex was broken
- Finch questioning whether it was worth touching something that already worked

Root presented the migration as possible but dangerous. The phrase “possible” was used in the same tone one might use for a bomb-disposal operation. The phrase “dangerous” was used with increasing confidence.

The initial risk classification was therefore elevated to: “High, but manageable if approached with appropriate ceremony.”

## Act II: The Gathering Storm

The preparation phase was extensive because the migration involved the Plex application, libraries, metadata, user state, paths, and service availability. The Committee did not want a casual move. It wanted a controlled systems handover, a metadata evacuation, and a dignified transfer from one host to another without anyone discovering that the old server still existed in a very inconvenient way.

Preparation included practical work that was, in hindsight, the reason the migration succeeded:

- confirm backups
- identify Plex configuration and metadata
- inspect current library paths
- confirm Reese could access Fusco media shares
- check permissions and ownership
- understand service startup
- prepare rollback options
- plan validation steps
- avoid deleting the old setup immediately
- preserve the ability to return Plex to Fusco if necessary

This was, as it turned out, the sensible part of the operation.

Root then escalated the plan into something more elaborate than the problem required. The Committee was introduced to a series of increasingly excessive safeguards:

- a backup of the backup
- a rollback plan for the rollback plan
- a pre-flight checklist for reviewing the pre-flight checklist
- a dedicated migration command centre
- colour-coded incident severity levels
- temporary dashboards for migration progress
- a formal coffee readiness assessment
- correlating cupboard temperature with Plex metadata transfer
- naming every migration phase
- a post-migration migration review
- a disaster simulation before the real migration

Finch repeatedly asked whether all of this was necessary. Root answered in the affirmative, but with the tone of someone who had already planned the ceremonial ribbon-cutting for the command centre.

The important point is that Root’s caution was valuable. Root was also, unfortunately, enjoying the complexity.

## Act III: Caffeine and Contingency

### Coffee Status

- Initial discussion: One cup
- Backup planning: Two cups
- Path validation: Elevated
- Pre-migration briefing: Operationally concerning
- Actual migration: Coffee largely forgotten because everything worked
- Post-migration: Celebration coffee authorised despite lack of crisis

Coffee became a recurring incident metric. One cup went cold while Root explained another contingency. Finch prepared coffee before any actual danger existed. More effort went into coffee preparation than into the final migration step, which was a powerful indicator that the Committee had decided to treat the whole thing as a prestige drama with a very small amount of actual risk.

No one was unsafe. Everyone was overprepared. That is a different category of problem and one that the Committee has since studied with great seriousness.

## Act IV: The Migration

The actual migration was conducted carefully and with the old setup kept available for rollback. The safe sequence was as follows:

1. Isolate or stop the old Plex instance to avoid concurrent confusion.
2. Confirm backup availability and retained configuration.
3. Transfer or restore Plex application data and metadata to Reese.
4. Configure Plex on Reese.
5. Confirm Fusco media mounts were available and usable.
6. Check library paths and permissions.
7. Start Plex on Reese.
8. Inspect the server and libraries.
9. Validate playback and watch state where confirmed.
10. Keep the old Fusco setup available temporarily as rollback insurance.

In practical terms, the migration was calm. The joke was that after all the buildup, the actual steps proceeded with suspicious ease.

## Act V: Suspicious Success

Plex started on Reese. Libraries appeared. Metadata appeared intact. Media paths worked. Playback worked. The server behaved normally. Nothing exploded.

The Committee, naturally, refused to accept success immediately.

Root insisted on further validation. Finch asked whether that meant one more check. Root said yes, but with the tone of a person who had already prepared a second round of validation in case the first round failed to be dramatic enough.

The following confirmations were considered important:

- Plex started successfully on Reese
- expected libraries appeared
- metadata and watch state appeared present as expected
- the Plex interfaces and libraries behaved normally
- playback worked
- the old Fusco setup remained available during the validation period

Plex itself appeared largely indifferent to the historic significance of the event.

## Act VI: The Doddle Revelation

The Committee eventually acknowledged the obvious truth: the migration was a doddle.

This was not because the project was trivial. It was because the preparation was thorough. Risks had been identified. Backups existed. Paths were checked. Mounts worked. Rollback remained available. The actual handover therefore behaved in a calm and professional manner.

Root resisted the word “doddle” until the evidence became overwhelming. By that point, every remaining argument had become an argument about tone rather than outcome.

## Official Historical Summary

Root had prepared for Mordor. Finch copied some files and restarted Plex.

The resulting migration was successful because the preparation covered the real risks, the old setup remained available until validation was complete, and the new host was able to provide the expected libraries and playback experience.

## Systems Involved

- Reese
- Fusco
- Plex
- Ubuntu
- Synology DSM
- SMB/CIFS mounts
- Plex metadata and configuration
- media libraries
- backups
- rollback plan
- monitoring
- Committee coffee supply

## Technical Risks Considered

The following risks were considered before the migration:

- metadata loss
- watch-history loss
- database corruption
- library path mismatch
- file permissions
- unavailable Fusco mounts
- incomplete application-data transfer
- server identity confusion
- remote access issues
- users seeing a broken server
- old and new Plex instances running simultaneously
- rollback failure

Not every listed risk occurred. They were the risks considered by the Committee before proceeding.

## Actions Taken

1. Reviewed the existing Plex deployment on Fusco.
2. Prepared backup and rollback options.
3. Confirmed Reese could access the required Fusco media shares.
4. Checked library paths, permissions, and related configuration assumptions.
5. Migrated Plex application data and metadata to Reese.
6. Configured the new host for Plex operation.
7. Started Plex on Reese.
8. Verified libraries, metadata, paths, and playback behaviour.
9. Kept the old Fusco setup available during validation.

## Validation

The following were verified as part of the migration process:

- Plex started on Reese
- expected libraries appeared
- metadata appeared intact
- media paths resolved correctly
- playback succeeded
- user and watch-state presence appeared intact where confirmed
- the old Fusco setup remained available during the validation period

## Outcome

- Plex successfully moved from Fusco to Reese
- Fusco remained the media-storage host
- Reese became the Plex application host
- users retained normal access
- playback worked
- the anticipated disaster did not occur
- the architecture became cleaner
- the migration was successful

## Mission Status

COMPLETED

## Casualties

- several cups of coffee
- one cold cup abandoned during contingency planning
- a large quantity of unnecessary dread
- multiple unused rollback scenarios
- Root’s hopes for a prestige disaster episode
- no metadata
- no watch history
- no media files
- no Plex libraries
- no actual casualties

## Lessons Learned

- preparation makes migrations look easy
- verify backups before touching the old instance
- understand paths and mounts
- keep rollback available until validation is complete
- test playback, not just service startup
- do not delete the old setup immediately
- a successful migration should look boring
- careful preparation is not wasted just because nothing went wrong
- Root can turn a file transfer into a six-act prestige drama
- coffee consumption is not a reliable measure of project difficulty
- Plex does not care about the emotional significance of its migration
- a lack of disaster is not evidence that preparation was unnecessary
- the phrase “one does not simply” may have oversold the difficulty
- the Committee will still hold a retrospective for an operation that worked first time
- Root will always retain one extra rollback plan “just in case”

## Official Findings

The Committee concluded that the Plex migration from Fusco to Reese succeeded. Preparation materially reduced risk, the anticipated catastrophe failed to attend, and the migration was completed without loss of the expected libraries, metadata, or playback functionality. Root’s contingency framework was technically defensible but dramatically excessive. Finch’s coffee consumption was inversely proportional to the amount of trouble encountered. Plex appeared indifferent to the historic importance of the event. Fusco handed over application duties while retaining storage responsibilities. Reese accepted Plex without complaint.

## Committee Findings

### Finch

> “Are we ready?”

### Root

> “Yes, but I have prepared for every possible failure mode, including the possibility that the migration is too successful for the emotional tone of the operation.”

### Finch

> “Is all of this necessary?”

### Root

> “Depends how committed you are to surviving the evening.”

### Fusco

> “I am still the storage host. The application is merely relocating.”

### Reese

> “I can host Plex. I have no opinion on the drama.”

### Plex

> “My libraries are here.”

### Health & Safety

> “Approved. The migration was conducted with appropriate preparation and no evidence of reckless improvisation.”

### Finance Department

> “How much of this planning budget was spent on coffee?”

### Root

> “That is not a meaningful question.”

## Final Verdict

### The migration was found:

- Not catastrophic
- Not destructive
- Not an all-weekend outage
- Not a metadata extinction event
- Not a watch-history apocalypse
- Not requiring the emergency command centre
- Mostly a careful transfer, path check, startup, and validation
- A doddle

### Root was found:

- Prepared
- Thorough
- Cautious
- Technically vindicated
- Dramatically disappointed
- Still looking for a hidden complication
- In possession of at least one unused rollback plan
- Unwilling to admit it was easy until formally outvoted

### Coffee was found:

- Present
- Excessive
- Increasingly ceremonial
- Poorly correlated with actual difficulty
- Essential to Committee morale
- Responsible for at least one unnecessary additional checklist

## Follow-On Operations

- Confirm Reese backup coverage for Plex configuration and related application data.
- Retire or archive the old Fusco Plex backup only after validation confirms the new host is stable.
- Check for containers or integrations still referencing the old Plex address or setup.
- Review Kometa and related integrations for old Plex references.
- Continue future disaster recovery documentation for Plex and related media services.
- Continue monitoring Plex on Reese after the migration.

## Series Status

Operation One Does Not Simply Migrate Plex entered production as a six-part prestige disaster series. It was cancelled during the pilot when Plex started, the libraries appeared, and playback worked. Root submitted a proposal for a second season titled Extended Metadata Validation. The Committee rejected it on the grounds that everyone wanted lunch.

## Best Quote

> “Root had prepared for Mordor. Finch copied some files and restarted Plex.”

## Related Documentation

- [Plex Runbook](/Runbooks/Plex)
- [Backups Runbook](/Runbooks/Backups)
- [Backups and Restore](/Infrastructure/Backups-and-Restore)
- [Network Map](/Infrastructure/Network-Map)
- [Operation Fusco, Open The Damn Door](/Operations/Operation-fusco-open-the-damn-door)
- [Operation Archive](/Operations/Operation-Archive)
- [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Canon](/Canon)
