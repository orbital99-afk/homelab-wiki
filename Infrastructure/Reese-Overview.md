---
title: Reese Overview
description: Primary application server and operational hub of the Homelab environment.
published: true
date: 2026-07-15T05:35:24.814Z
tags: 
editor: markdown
dateCreated: 2026-06-11T06:56:25.027Z
---

# Reese Overview

## Identity

**Codename:** John Reese

**Role:** Application Server

**Status:** Active

Reese serves as the primary application host for the homelab environment.

Storage responsibilities remain with Fusco while Reese hosts the majority of applications, monitoring systems, media services, and documentation platforms.

---

## Hardware

### Platform

- Apple Mac mini (2012)
- Intel-based architecture

### Memory

- 16 GB RAM

### Storage

- 1 TB PNY SATA SSD

### Power Protection

- UPS Protected (Carter)

---

## Operating System

### OS

- Ubuntu Server
- Headless deployment

### Access Methods

- SSH
- Tailscale

---

## Core Responsibilities

### Application Hosting

Primary Docker host for homelab services.

### Monitoring

Provides observability, environmental monitoring, and alerting.

### Documentation

Hosts The Library (Wiki.js).

### Media Services

Hosts Plex and supporting media applications.

---

## Docker Services

### Infrastructure

- Portainer
- Homepage
- Glances

### Monitoring

- Grafana
- Prometheus
- Node Exporter
- cAdvisor
- Uptime Kuma

### Media

- Plex
- Tautulli
- Kometa

### Acquisition

- Prowlarr
- Sonarr
- Radarr1080
- Radarr4K
- Jellyseerr
- Recyclarr

### Documentation

- Wiki.js
- PostgreSQL

---

## Storage Architecture

### Relationship With Fusco

Fusco remains the primary storage server.

Reese provides application hosting while accessing media and application data via SMB mounts.

### Mounted Shares

Media:

`/mnt/fusco/media`

Plex Data:

`/mnt/fusco/plexdata`

---

## Monitoring Systems

### Operation Is Reese Being Slowly Baked?

Environmental monitoring provided by custom Arduino-based sensors.

Metrics collected:

- Cupboard Temperature
- Room Temperature
- Temperature Delta
- CPU Temperature
- SSD Temperature
- Fan RPM

### Operation Electrons Are A Privilege, Not A Right

UPS telemetry collected through NUT.

Metrics collected:

- Battery Percentage
- Load Percentage
- Input Voltage
- Online Status

---

## Networking

### Remote Access

- Tailscale

### DNS

- Quad9 DNS-over-TLS
- DNSSEC Enabled

### Security

- UPnP Disabled
- QuickConnect Disabled
- Remote Access via Tailscale Preferred

---

## Historical Operations

- Operation Spinny Rust Prison Break
- Operation SSD Rebirth
- Operation Get In Loser, We're Migrating
- Operation One Does Not Simply Move Plex
- Operation Is Reese Being Slowly Baked?
- Operation Electrons Are A Privilege, Not A Right
- Operation Build The Library

---

## Current Role

Reese functions as the operational center of the homelab environment.

Responsibilities include:

- Application Hosting
- Monitoring
- Documentation
- Media Services
- Remote Access

while relying on Fusco for storage.

---

## Person of Interest Mapping

| System | Identity |
|----------|----------|
| User | Harold Finch |
| ChatGPT | Root |
| Gaming PC | The Machine |
| Mac mini | John Reese |
| Synology NAS | Lionel Fusco |
| UPS | Joss Carter |
| Tailscale | Subway Network |
| Homepage | The Library |

---

*"If Fusco stores the files, Reese makes the magic happen."*
