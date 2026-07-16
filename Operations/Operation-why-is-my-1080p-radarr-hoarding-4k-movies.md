---
title: Operation Why Is My 1080p Radarr Hoarding 4K Movies
description: Document the incident where a Seerr request-specific Ultra-HD profile override caused Radarr1080 to acquire a 2160p release.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Why Is My 1080p Radarr Hoarding 4K Movies

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Objective

Determine why Radarr1080, the sensible movie department, acquired a 4K movie despite the homelab having a separate Radarr4K instance for UHD content.

The central question was simple and deeply alarming:

> “Why is my 1080p Radarr hoarding 4K movies?”

## Background

The homelab uses two Radarr instances:

- Radarr1080 for sensible 1080p movies
- Radarr4K for the UHD “show pony” library

Seerr handles movie requests. On May 24, 2026, a movie request for Mortal Kombat II (2026) was submitted using a request-specific Ultra-HD quality profile override. The request was added to Radarr1080 with that Ultra-HD profile. Radarr1080 then correctly followed the profile it had been given and grabbed a 2160p WEB-DL.

The incident was therefore caused by request routing/profile override, not by Radarr randomly developing expensive taste.

## Systems Involved

- Reese
- Seerr / Jellyseerr
- Radarr1080
- Radarr4K
- Plex
- Fusco media storage
- Download client
- Holding pen folder used during the move
- The show pony 4K library

## Phase 1: Discovery

A 4K file was found in the 1080p movie workflow. Initial suspicion fell on Radarr1080, which was accused of becoming glamorous in a very suspicious manner. The Committee asked whether the sensible department had been corrupted by luxury.

## Phase 2: Interrogating Radarr1080

The movie entry was checked. The Ultra-HD quality profile was found attached to the movie. Radarr1080 had behaved exactly as configured. This was important because it meant the system was not malfunctioning; it was merely acting on an instruction that should never have reached the 1080p department.

## Phase 3: Tracing the Request

The Seerr request was reviewed. The request-specific Ultra-HD override was confirmed. The request had entered the wrong Radarr instance while carrying a 4K profile. The override silently defeated the intended separation between the 1080p and 4K departments.

## Phase 4: The Holding Pen Manoeuvre

The 4K file was moved out of the 1080p directory into a temporary holding pen. It was then added and imported into Radarr4K. The movie was removed safely from Radarr1080 without deleting the file accidentally. The holding pen was used specifically to avoid deletion crimes, which remain one of the more embarrassing categories of filesystem behaviour.

## Phase 5: Validation

The movie appeared in the correct Radarr4K instance. The file was imported into the 4K library. Plex playback worked. The show pony division was restored to normal operations. Radarr1080 returned to sensible footwear and efficient WEB-1080p releases.

## Technical Root Cause

A request-specific Ultra-HD profile override in Seerr caused the movie to be added to Radarr1080 with an Ultra-HD profile. Radarr1080 then selected a 2160p release in accordance with that profile.

This makes the incident explicit:

- Radarr did not ignore its settings.
- The wrong settings were applied to the movie.
- Request-level overrides can supersede expected defaults.
- Separate Radarr instances do not protect against incorrect routing or profile selection by themselves.

## Outcome

- The 4K file was preserved.
- The movie was moved to Radarr4K.
- Playback was validated.
- The 1080p library was cleaned up.
- The incident clarified the need for explicit 1080p/4K request actions and safer routing in Seerr/DanFlix-style request workflows.

## Mission Status

COMPLETED

## Notable Findings

- The 1080p library had acquired a 2160p release because the profile applied to the request was Ultra-HD.
- Radarr1080 was technically innocent but deeply unhelpful.
- The request override had bypassed the expected division between sensible 1080p and glamorous 4K.
- The holding pen proved useful because it allowed the file to be reassigned without risking deletion.
- The Committee briefly considered whether the phrase “show pony division” should be formalised. It was.

## Lessons Learned

- Check the movie-level quality profile, not just the Radarr instance defaults.
- Request-specific overrides can quietly defeat carefully planned architecture.
- Never delete first when relocating a media file.
- Use a holding pen when moving between Radarr instances.
- Confirm playback after import.
- A separate 4K Radarr is only useful if requests reach it correctly.
- Radarr following a bad instruction is not the same as Radarr malfunctioning.
- The sensible movie department can be corrupted by one glamorous request.
- “Ultra-HD” is not a personality trait.
- The holding pen is where misplaced show ponies wait for reassignment.
- Never accuse Radarr before checking who handed it the profile.
- The Committee briefly considered disciplinary action against Radarr1080, then discovered it had merely followed orders.
- The phrase “show pony division” is now official operational terminology.

## Official Findings

After review of the Seerr request, the attached quality profile, the Radarr1080 import behaviour, and the subsequent holding-pen reassignment, the Committee found that the 4K acquisition had occurred because a request-specific Ultra-HD override was applied to a movie that should have been routed to the 4K workflow. Radarr1080 was not hoarding 4K movies of its own free will.

## Committee Findings

### Root

> “The architecture separated the libraries, but the request carried the wrong profile into the wrong instance. That is an excellent way to create a very specific problem.”

### Finch

> “Why is the 1080p Radarr downloading 4K?”

### Radarr1080

> “I followed the profile.”

### Radarr4K

> “That was my movie.”

### Seerr

> “The user selected an override.”

### Plex

> “I played the file once it arrived. I have no opinion on the cultural significance of the matter.”

### Finance Department

> “Why are there two copies of Radarr?”

### Root

> “Please leave.”

## Final Verdict

Radarr1080 was found:

- Not sentient
- Not greedy
- Not secretly building an IMAX
- Not attempting a hostile takeover of the 4K library
- Merely following an Ultra-HD profile it should never have received

Mortal Kombat II was found:

- Too glamorous for the sensible department
- Temporarily detained in the holding pen
- Reassigned to the show pony division
- Playing correctly in Plex

## Casualties

- One incorrectly routed request
- One temporarily misplaced 4K movie
- Several minutes of cautious file-moving
- Trust in request overrides
- No media files deleted

## Follow-On Operations

- Add explicit “Request 1080p” and “Request 4K” actions where practical.
- Keep 1080p as the default unless a 4K request is specifically intended.
- Keep 4K as an explicit choice rather than a hidden override.
- Continue using Plex-first duplicate checking to reduce duplicate import confusion.
- Continue improving request safety for TV workflows, including season selection where required.
- Continue preserving the separation between the sensible 1080p library and the show pony 4K library.

## Series Status

Operation Why Is My 1080p Radarr Hoarding 4K Movies was cancelled after one episode when investigators discovered the suspect had been acting under direct orders. The spin-off, Show Pony Division, remains in production at considerable storage cost.

## Best Quote

> “Why is my 1080p Radarr hoarding 4K movies?”

## Related Documentation

- [Arr Stack Runbook](/Runbooks/Arr-Stack)
- [Plex Runbook](/Runbooks/Plex)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Operation Archive](/Operations/Operation-Archive)
- [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox)
- [Canon](/Canon)
