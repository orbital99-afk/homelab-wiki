---
title: Network Map
description: Physical and logical map of the homelab network and remote-access paths.
published: true
date: 2026-07-15T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-15T00:00:00.000Z
---

# Network Map

## Physical Layout

The ASUS TUF-AX5400 is the primary router. ZenWiFi XD4 access points extend wireless coverage using wired backhaul, avoiding the traditional ritual of sacrificing half the bandwidth to mesh traffic.

Unmanaged switches provide local Ethernet distribution in:

- Office
- Bedroom
- Garage
- Lounge

Reese, the 2012 Mac mini and primary application host, lives in the garage cupboard. Fusco is the Synology NAS and provides storage and media shares to Reese.

## Logical Layout

```text
Internet
   |
ASUS TUF-AX5400
   |
   +-- ZenWiFi XD4 access points (wired backhaul)
   +-- Office / Bedroom / Garage / Lounge switches
                         |
                         +-- Reese (applications)
                         +-- Fusco (storage)
```

Elias (Tailscale) provides private remote access for authorised devices. It is the preferred route into the homelab; do not expose a service publicly merely because typing a VPN command felt inconvenient.

## Naming and Reverse Proxy Goal

The friendly-name and reverse-proxy goal is to reach services with memorable local names rather than ports, including:

- `grafana.reese`
- `sonarr.reese`
- `seer.reese`

Treat these as target names until DNS and reverse-proxy configuration confirm they are live. Record addresses, certificates, and exceptions here when implemented.
