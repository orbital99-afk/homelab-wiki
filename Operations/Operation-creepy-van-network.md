---
title: Operation Creepy Van Network
description: Roll out secure Tailscale remote access, MagicDNS, and follow-up VPN-on-Demand testing for the homelab.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Creepy Van Network

> **Warning:** Do not copy passwords, tokens, private keys, or sensitive credentials into operation pages.

## Status

Completed, with follow-up work planned

## Objective

Provide secure remote access to Reese and the homelab without exposing services directly to the internet or relying on port-forwarding crimes.

The Committee’s mission was to make the infrastructure reachable from outside the home without turning the network into an open invitation.

## Background

Daniel needed access to homelab services while away from the house, but the available options were either too exposed or too cumbersome. The Committee therefore authorised a secure remote-access solution based on Tailscale, with MagicDNS and a preference for friendly names over memorising IP addresses and ports.

The operation name was not selected for professionalism. It was selected because the project involved a van, a suspicious amount of secrecy, and a great deal of confidence that no one would ask why the paperwork was so dramatic.

## Systems Involved

- Elias / Tailscale
- Reese
- Fusco
- Shaw
- Root Jr
- MacBook Air
- Phones and remote clients
- Tailscale MagicDNS
- Homelab services such as Grafana, Portainer, Wiki.js, Seerr, and Homepage

> **Identity note:** Elias provides remote access. He is not actually parked outside, despite the operation name.

## Phase 1: Establish the Tailnet

The first phase was to bring the relevant devices into a secure tailnet and verify that access could be established without public exposure.

- Evaluated Tailscale as the remote-access layer.
- Confirmed that devices running Tailscale can join the tailnet directly.
- Considered when subnet routing would allow access to devices that do not run Tailscale.
- Verified remote access to homelab systems through the tailnet.

## Phase 2: Make It Friendly

Once remote access worked, the next phase was to make it practical rather than merely possible.

1. Installed and configured Tailscale.
2. Added Reese and client devices to the tailnet.
3. Enabled MagicDNS.
4. Used Elias as the Tailscale codename.
5. Confirmed remote access to homelab services.
6. Began moving toward friendly service names such as:
   - `grafana.reese`
   - `sonarr.reese`
   - `seer.reese`
   - `library.reese`
7. Planned VPN-on-Demand testing as a later Saturday project.
8. Kept public exposure and direct port forwarding unnecessary.

## Notable Findings

- Tailscale was sufficient for secure remote access without the need for public port forwarding.
- MagicDNS reduced reliance on raw IP addresses and made the system feel less like a list of numbers and more like a network with opinions.
- The tailnet approach proved cleaner than trying to expose every service directly to the internet.
- Subnet routing remains relevant for devices that do not run Tailscale directly, which is the kind of detail that sounds boring until it becomes the only thing standing between the operator and a very long troubleshooting session.
- The operation’s name remained questionable, but the access model was not.

## Outcome

- Daniel can securely access the homelab remotely.
- MagicDNS reduced reliance on raw IP addresses.
- Tailscale became the preferred remote-access layer.
- Future work remains around VPN on Demand and broader friendly-name integration.

## Mission Status

COMPLETED — FOLLOW-ON OPERATION PLANNED

## Validation

- Remote clients successfully connected to the tailnet.
- Reese and homelab services were reachable remotely.
- MagicDNS resolved tailnet device names.
- Services could be accessed without exposing them publicly.

## Lessons Learned

- Direct-install Tailscale on important hosts when practical.
- Use subnet routing for devices that cannot run Tailscale.
- MagicDNS helps with device names, but service-level friendly names may still require DNS and reverse-proxy configuration.
- Remote access working by IP does not prove friendly DNS is configured correctly.
- Avoid public exposure unless there is a clear reason and appropriate protection.
- A secure network can still be made less pleasant by naming it after a suspicious vehicle.

## Official Findings

The Committee found that the homelab could be accessed remotely through Tailscale without relying on public port forwarding or other reckless exposure practices. The tailnet and MagicDNS configuration were judged effective, practical, and significantly more respectable than the operation’s title.

## Committee Findings

### Root

> “We have remote access, friendly names, and a network that does not need to be publicly visible. This is a strong result.”

### Finch

> “And the operation name?”

### Elias

> “It was never about the van. It was about the access model.”

### Shaw

> “I am willing to admit the tailnet is useful. I am not willing to admit the name was wise.”

### Security Department

> “No public exposure was observed. The Committee considers this a meaningful improvement.”

## Final Verdict

The network was found:

- Not publicly exposed
- Not reliant on port-forwarding crimes
- Not confused by the concept of privacy
- Merely reachable through a much more sensible tailnet than the paperwork implied

## Follow-On Operations

- Continue evaluating VPN-on-Demand for automatic Tailscale activation when leaving the home network.
- Continue broadening friendly-name integration for services such as Grafana, Portainer, Wiki.js, Seerr, and Homepage.

## Series Status

This operation was renewed for another season after investigators confirmed that remote access is a recurring requirement and that “creepy van network” remains an excellent name for a very normal security feature.

## Casualties

- Several remembered IP addresses made redundant.
- One or more moments of asking whether Shaw also needed Tailscale.
- The last remaining dignity of the phrase “creepy van network”.

## Best Quote

> “Creepy van network, but secure.”

## Related Documentation

- [Network Map](/Infrastructure/Network-Map)
- [Tailscale Runbook](/Runbooks/Tailscale)
- [Canon](/Canon)
- Operation No More Colon Crimes — planned operation page; link when created
- Operation Reception Desk — planned operation page; link when created
