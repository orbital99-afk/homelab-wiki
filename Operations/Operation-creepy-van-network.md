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

## Mission Brief

Provide secure remote access to Reese and the homelab without exposing services directly to the internet or relying on port-forwarding crimes.

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

## The Problem

- Daniel needed secure remote access to homelab services from outside the home network.
- Direct port forwarding was undesirable.
- Friendly access names were preferable to remembering IP addresses and ports.
- There was uncertainty about whether every device needed Tailscale installed or whether subnet routing could cover local devices.
- Remote access needed to remain simple enough to use from phones and Macs.

## Investigation

- Evaluated Tailscale as the remote-access layer.
- Confirmed that devices running Tailscale can join the tailnet directly.
- Considered when subnet routing would allow access to devices that do not run Tailscale.
- Tested MagicDNS for friendly device names.
- Discussed VPN on Demand for automatically enabling Tailscale when leaving the home network.
- Verified remote access to homelab systems through the tailnet.

## Actions Taken

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

## Outcome

- Daniel can securely access the homelab remotely.
- MagicDNS reduced reliance on raw IP addresses.
- Tailscale became the preferred remote-access layer.
- Future work remains around VPN on Demand and broader friendly-name integration.

## Validation

- Remote clients successfully connected to the tailnet.
- Reese and homelab services were reachable remotely.
- MagicDNS resolved tailnet device names.
- Services could be accessed without exposing them publicly.

## Casualties

- Several remembered IP addresses made redundant.
- One or more moments of asking whether Shaw also needed Tailscale.
- The last remaining dignity of the phrase “creepy van network”.

## Lessons for Future Daniel

- Direct-install Tailscale on important hosts when practical.
- Use subnet routing for devices that cannot run Tailscale.
- MagicDNS helps with device names, but service-level friendly names may still require DNS and reverse-proxy configuration.
- Remote access working by IP does not prove friendly DNS is configured correctly.
- Avoid public exposure unless there is a clear reason and appropriate protection.

## Best Quote

> “Creepy van network, but secure.”

## Related Documentation

- [Network Map](/Infrastructure/Network-Map)
- [Tailscale Runbook](/Runbooks/Tailscale)
- [Canon](/Canon)
- Operation No More Colon Crimes — planned operation page; link when created
- Operation Reception Desk — planned operation page; link when created
