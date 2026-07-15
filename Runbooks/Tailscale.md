---
title: Elias Tailscale Runbook
description: Health checks and recovery guidance for private remote access through Tailscale.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Elias / Tailscale Runbook

> **Warning:** If unsure, inspect before restarting. If still unsure, ask Root before committing crimes.

## Purpose

Elias is Tailscale, the secure creepy-van network that provides private remote access to Reese and authorised devices.

## Where It Lives

- Reese runs the Tailscale client on Ubuntu.
- Authorised remote devices also run Tailscale.
- Name resolution may involve Tailscale MagicDNS and local DNS configuration.

## Quick Health Check

```bash
tailscale status
systemctl status tailscaled
```

Confirm Reese appears online from another authorised device. Test connectivity by Tailscale name or address, then distinguish a Tailscale failure from a service, firewall, or DNS failure.

## Restart Procedure

1. Run `tailscale status` and inspect the `tailscaled` service state and recent logs.
2. Confirm the local network and internet connection are working.
3. If the daemon is unhealthy, restart it with `sudo systemctl restart tailscaled`.
4. Run `tailscale status` again and test access from an authorised peer.
5. Re-authenticate only when required; do not replace working identity state as a first diagnostic step.

## Common Goblins

- **DNS Goblin:** Peer connectivity works by address but not by name.
- **Expired or removed identity:** Reese no longer appears as an authorised device.
- **Local network failure:** Tailscale is blamed for an upstream connectivity problem.
- **Firewall or route issue:** The peer is online, but the intended service or subnet is unreachable.

## Do Not Casually Delete

Do not remove Reese from the tailnet, erase Tailscale state, rotate keys, or change routes and access controls without confirming the recovery path. Remote access is a poor service to lock while standing outside the door.

## Related Pages

- [Network Map](/Infrastructure/Network-Map)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Monitoring Runbook](/Runbooks/Monitoring)
- [Disaster Recovery: Reese Dies](/Operations/Disaster-Recovery-Reese-Dies)
- [Known Goblins](/Case-files/Known-Goblins)
