---
title: Operation Build The Library
description: Create a central documentation platform for the Reese homelab environment.
published: true
date: 2026-07-15T05:35:21.537Z
tags: 
editor: markdown
dateCreated: 2026-06-11T06:14:47.038Z
---

Operation Build The Library

Objective

Create a central documentation platform for the Reese homelab environment.

Background

As the homelab expanded, knowledge became distributed across chat histories, text files, notes, and memory. A dedicated documentation system was required to preserve operational knowledge and provide a searchable archive.

Implementation

Platform

* Wiki.js
* PostgreSQL

Host

* Reese (Ubuntu Server)
* Docker Compose deployment

Deployment Notes

* PostgreSQL database deployed successfully.
* Wiki.js container deployed successfully.
* Initial port conflict encountered with Grafana.
* Wiki.js reassigned to port 3003.
* Service verified operational.

Initial Structure

The Library was established with the following sections:

* Operations
* Infrastructure
* Seedbox
* Future Projects
* Case Files
* Ancient Texts

First Milestone

* Home page created.
* Operations page created.
* First internal navigation link established.

Outcome

The Library became the official documentation repository for the homelab environment.

Status

Completed

Date

June 2026

⸻

“Knowledge is useful only if it survives the next reboot.”
