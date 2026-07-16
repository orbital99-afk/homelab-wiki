---
title: Operation No More Colon Crimes
description: Replace raw host-and-port service addresses with memorable local names through distinct DNS and reverse-proxy layers.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation No More Colon Crimes

> **Status:** Active foundation completed, with follow-on work continuing

> **Scope note:** Names ending in `.reese` are intended as local or tailnet homelab names. `.reese` is not documented as a publicly registered internet domain, and the names below remain targets until DNS and reverse-proxy validation confirms each one is live.

## Objective

Replace human-facing homelab addresses based on raw hostnames or IP addresses plus port numbers with memorable service-specific names.

Practical objectives:

- reduce reliance on memorised port numbers
- make services easier to open from browsers and bookmarks
- improve consistency across local and remote access
- separate human-facing service names from backend container details
- use local DNS for name resolution
- use reverse proxying for service routing where required
- preserve secure remote access through Elias / Tailscale
- document the naming architecture
- prevent Future Daniel from asking which unexplained number belongs to Grafana

The Committee issued its central declaration:

> “The ports may remain. The colons will no longer govern us.”

## Background

The homelab had become sophisticated enough to include Plex, Sonarr, Radarr1080, Radarr4K, Seerr, Grafana, Prometheus, Portainer, Uptime Kuma, Homepage, Wiki.js, and other services.

It had dashboards, monitoring, automated reports, environmental sensing, UPS telemetry, remote access, and media automation. It did not have the ability to remember which port opened which page without consulting notes, browser history, or the oral tradition maintained by whichever person last touched Docker.

Access still often resembled:

```text
some-host:some-number
```

This was technically valid and operationally functional. It was also visually suspicious, hostile to bookmarks, dependent on port-number folklore, and indistinguishable from coordinates supplied during a hostage negotiation.

The Committee classified the matter as an architectural dignity issue and opened a formal inquiry around one central question:

> “Why does every service address look like a warehouse loading bay followed by an extension number?”

## Incident Classification

- **Offence:** Unnecessary colon exposure
- **Crime scene:** Browser address bar
- **Victims:** Finch, Future Daniel, bookmarks, human memory
- **Suspects:** Docker ports, incomplete DNS, absent reverse proxy
- **Aggravating factor:** Numbers with no obvious connection to the service
- **Repeat offender:** Every container with a web interface
- **Proposed rehabilitation:** Friendly DNS names and Caddy
- **Maximum sentence:** Permanent concealment behind the reception desk

## Act I: The Port Number Era

Before friendly service names, web services were commonly reached through a host address followed by the service's published port. Each service had a different backend destination. Those numbers mattered to Docker, the host, and the application configuration; they meant almost nothing to the person trying to open a dashboard.

Browser history became a primitive service catalogue. Bookmarks performed work that should have belonged to the addressing architecture. Finch could remember some port numbers, but not enough to approach the address bar with confidence. Root repeatedly said “open the service on port…” as if this were an acceptable level of civilisation.

One wrong digit could produce:

- the wrong service
- no service
- a refusal to connect
- a brief period of accusing DNS despite not using DNS

After reviewing the evidence, the Committee declared:

> An address can be technically correct and still look like a crime.

## Act II: Naming the Establishment

The proposed service-specific names included:

- `library.reese`
- `grafana.reese`
- `sonarr.reese`
- `seer.reese`

These are memorable, self-explanatory, easy to bookmark, and independent of the backend port. They fit the homelab canon, reduce terminal archaeology, and make the infrastructure feel like a place rather than a list of socket assignments.

Reese identifies the primary application host. The prefix identifies the service Finch intends to visit. Several names can lead toward Reese while still describing different destinations inside it.

The repository documents these as friendly-name goals. It does not yet establish that every proposed name is operational on every local and tailnet client.

## Act III: DNS Is Asked to Provide Directions

DNS performs name resolution. A suitable local DNS service, host records, or client-visible DNS configuration can make names such as `grafana.reese` and `library.reese` resolve to Reese's address. Multiple service names may resolve to the same host, removing the need for a human to type or remember Reese's raw address.

DNS can:

- resolve a friendly service name to Reese's address
- point several service names at the same host
- reduce dependence on raw IP addresses
- provide the first half of the friendly-navigation experience

DNS cannot, by itself:

- decide that `grafana.reese` belongs to Grafana's backend port
- decide that `library.reese` belongs to Wiki.js's backend port
- replace HTTP routing when several web services share one host
- read the Committee's intentions
- distinguish containers based solely on optimism

Once DNS has directed the request to Reese, something must inspect the requested hostname and send the request to the correct service.

> DNS knew where the building was. It did not know which office Finch wanted.

## Act IV: Elias and MagicDNS Testify

Elias / Tailscale provides secure remote transport into the homelab. MagicDNS is enabled and helps tailnet clients resolve device names. That makes device-level addressing friendlier and reduces reliance on raw IP addresses.

MagicDNS does not automatically create separate service-level reverse-proxy routes for every container on Reese. It can help a client find a device; it does not decide which web application behind that device should answer a particular hostname.

> Elias could get Finch onto the property. He was not the receptionist.

Depending on the final design, local DNS, Tailscale DNS configuration, host overrides, or another suitable naming layer may still be needed to make names such as `grafana.reese` available to each client. Local and tailnet clients may use different resolvers, so success on one device does not establish success everywhere.

## Act V: The Reception Desk Proposal

Caddy was selected as the intended reception desk for the related **Operation Reception Desk**. That operation deserves its own complete page; this page records why it is required and how its role differs from DNS.

As a reverse proxy, Caddy can:

- listen for web requests
- inspect the requested hostname
- route `grafana.reese` to the Grafana backend
- route `library.reese` to the Wiki.js backend
- route `sonarr.reese` to the Sonarr backend
- keep backend ports out of the human-facing address
- centralise hostname-to-service routing
- manage HTTP or HTTPS behaviour where appropriately configured

No exact routes, ports, certificates, or Caddyfile entries are asserted here. Those details must come from the implemented configuration and its documentation.

Caddy is the receptionist, switchboard, and front desk: professionally unimpressed by visitors asking for “whatever lives on that random port,” but fully capable of directing a hostname to the office containing the correct container.

## Act VI: The Colon Tribunal

The Committee convened a tribunal to decide whether the punctuation itself was responsible or merely present at every crime scene.

### Charges Against the Colon

- appearing in every service address
- introducing an unexplained number
- undermining visual elegance
- forcing Finch to remember backend implementation details
- making bookmarks resemble evidence
- encouraging copy-and-paste dependency
- exposing infrastructure plumbing to innocent browser users

### Defence of the Colon

- ports are technically required
- the colon is valid URI syntax
- backend services still need destinations
- Docker did not create the addressing standard
- the colon was only following protocol

### Committee Ruling

The colon is not abolished from networking. It is removed from routine human-facing access wherever practical. Backend services may retain ports; the frontend shall present names.

> “The colon was found technically innocent but aesthetically guilty.”

## Technical Architecture

The intended local request path is:

```text
Browser
  → friendly service name
  → DNS resolution
  → Reese
  → Caddy / reverse proxy
  → correct backend service and port
```

The intended remote request path is conceptually:

```text
Remote client
  → Elias / Tailscale
  → DNS resolution available to the client
  → Reese
  → Caddy / reverse proxy
  → requested service
```

The exact DNS path may differ between local LAN clients, tailnet clients, devices using router-provided DNS, and devices using a future local DNS service. The final resolver and record design must be documented after implementation rather than inferred from the desired names.

## Systems Involved

- Reese
- Docker
- Caddy
- Elias / Tailscale
- MagicDNS
- local DNS or host records
- ASUS TUF-AX5400 router
- ZenWiFi access points where relevant
- Wiki.js / The Library
- Grafana
- Sonarr
- Seerr
- other web services
- browsers and bookmarks
- Committee Department of Addressing Standards
- HR / YAML configuration risk

## Practical Benefits

- memorable addresses
- easier bookmarks
- simpler documentation
- backend ports can change without changing the user-facing name
- improved consistency
- easier onboarding of Future Daniel
- cleaner remote access
- service names that communicate purpose
- reduced accidental navigation to the wrong application
- less terminal archaeology
- easier linking from The Library

Friendly names do not replace monitoring, authentication, access controls, backups, correct DNS configuration, reverse-proxy configuration, or certificate planning where HTTPS is used. A pleasant name is an interface improvement, not a security control and not a substitute for operating the service properly.

## Technical Risks Considered

The following are risks to consider, not a claim that all have occurred:

- DNS records pointing to the wrong address
- local and remote clients using different DNS resolvers
- assumptions that MagicDNS provides service routing
- reverse-proxy routing mistakes
- hostname collisions
- Caddy not starting
- a backend service being unavailable
- incorrect backend ports
- HTTP versus HTTPS confusion
- browser caching
- stale DNS
- Reese changing between wired and wireless addresses during a power incident
- friendly names working on one device but not another
- circular blame involving DNS, Caddy, Docker, and the browser
- YAML or Caddyfile configuration crimes

## Actions Taken or Planned

The repository confirms the secure remote-access foundation, MagicDNS, the desired naming convention, and the intended DNS-plus-reverse-proxy architecture. It does not yet confirm complete service-name rollout or end-to-end Caddy validation.

| Step | Action | Status |
| --- | --- | --- |
| 1 | Inventory services and current access methods | Active |
| 2 | Choose consistent friendly names | Foundation completed; broader naming remains active |
| 3 | Decide which DNS layer will resolve the names | Planned / design to be documented |
| 4 | Point service hostnames toward Reese | Planned or active; not confirmed complete |
| 5 | Deploy or configure Caddy as the reverse proxy | Planned under Operation Reception Desk |
| 6 | Define hostname-to-backend mappings | Planned |
| 7 | Test locally | Planned where each name is configured |
| 8 | Test through Elias / Tailscale | Planned where each name is configured |
| 9 | Verify bookmarks and documentation | Planned |
| 10 | Document troubleshooting procedures | Active through this operation; implementation detail planned |
| 11 | Preserve direct port access temporarily for diagnosis | Planned rollout policy |
| 12 | Remove colon-dependent habits after validation | Planned and emotionally overdue |

GitHub remains the source of truth for The Library, and Wiki.js presents the documentation. Configuration truth must still be checked against the actual DNS and reverse-proxy implementation.

## Validation

Validation for each friendly name should confirm:

- the name resolves to Reese for the client being tested
- Caddy receives the request
- the correct backend service opens
- the wrong service does not open
- local access works
- remote access works where configured
- direct backend access remains available for troubleshooting during rollout
- service links in The Library are accurate
- browser caching or stale DNS is not masking the result

Confirmed today: Elias provides remote access, MagicDNS resolves tailnet device names, and Reese-hosted services are reachable remotely. Not yet claimed here: complete DNS, proxy, local-client, and remote-client validation for every proposed `.reese` service name.

## Outcome

- the architecture for friendly service names was established
- GitHub and The Library document the intended naming system
- raw ports were designated backend implementation details rather than preferred navigation
- Caddy was selected as the intended reception desk
- Elias remained the secure remote transport layer
- MagicDNS remained useful for device names
- service-level names were correctly identified as requiring cooperation between DNS and reverse proxying
- implementation and refinement remain ongoing
- the Committee formally began removing colon crimes from daily life

The core conclusion was unanimous:

> Ports remained technically necessary, but the Committee determined they did not need to be exposed to Finch’s eyeballs.

## Mission Status

**ACTIVE FOUNDATION COMPLETED — COLON REHABILITATION CONTINUES**

> Direct port access remains available under controlled conditions for troubleshooting, legacy bookmarks, and moments when the reception desk has gone to lunch.

## Help Guide

# How to Turn an Advanced Homelab Into a List of Hostage Coordinates

### Step 1: Deploy multiple sophisticated services

Install monitoring, media automation, dashboards, remote access, and documentation.

### Step 2: Assign each service a port

Allow Docker and application defaults to establish a numerical folklore system.

### Step 3: Refuse to create friendly names

Insist that memory and browser history are adequate infrastructure.

### Step 4: Ask Finch to remember all the numbers

Observe confidence degrade immediately.

### Step 5: Add more services

Ensure previous port knowledge becomes obsolete before it can become useful.

### Step 6: Document each address in several unrelated places

Create the illusion of organisation.

### Step 7: Finally deploy DNS and Caddy

Discover that services can be addressed like places rather than evidence-locker references.

### Step 8: Declare the colons internal matters

Allow the backend to retain its numerical secrets.

## Official Port Rehabilitation Programme

| Former Public Identity | Rehabilitated Identity | Current Role |
| --- | --- | --- |
| Reese plus unexplained Wiki.js port | `library.reese` | Institutional memory |
| Reese plus unexplained Grafana port | `grafana.reese` | Pretty panic |
| Reese plus unexplained Sonarr port | `sonarr.reese` | Television acquisition |
| Reese plus unexplained Seerr port | `seer.reese` | Request desk |
| Reese plus assorted other numbers | Future friendly names | Pending rehabilitation |

> Backend ports have been withheld to protect operational dignity and because they may vary.

## Coffee Status

- Service inventory: One cup
- Naming debate: Second cup
- DNS explanation: First cup reheated
- Reverse proxy explanation: New cup authorised
- First friendly address opens: Victory coffee
- Browser cache causes one inconsistent result: Coffee replaced by interpretive swearing

## Casualties

- several raw bookmarks
- trust in human port-number memory
- one browser history used as infrastructure documentation
- multiple colons exposed to public ridicule
- several backend ports reassigned to non-public duties
- Root's habit of saying “just use the port”
- no services
- no containers
- no standards-compliant URI syntax
- no actual punctuation harmed

## Lessons Learned

### Technical Lessons

- DNS resolves names to addresses.
- Reverse proxies route requests to services.
- MagicDNS is helpful but is not the entire service-routing solution.
- Friendly names should be documented consistently.
- Test local and remote DNS paths separately.
- Retain direct backend access during rollout.
- Use one naming convention.
- Avoid embedding backend ports into permanent user workflows.
- Browser and DNS caches can mislead testing.
- Service names should describe purpose.
- A reverse proxy becomes critical infrastructure once navigation depends on it.
- Document how to bypass the proxy during troubleshooting.

### Committee Lessons

- An advanced homelab should not require a port-number oral tradition.
- Browser history is not a service catalogue.
- A colon followed by four digits is not a memorable product name.
- Ports are plumbing and should remain behind the wall.
- Elias is transport, not reception.
- DNS can locate the building but cannot escort Finch to Grafana.
- Caddy is the first component hired primarily for customer service.
- Every backend port believes it is important until hidden behind a friendly name.
- Root must stop presenting socket addresses as if they are charming.
- Future Daniel deserves URLs that resemble words.
- Punctuation can be technically correct and still require intervention.

## Official Findings

The Committee finds that raw host-and-port addresses were functional but insufficiently humane. Friendly service names improve usability, bookmarks, and documentation. DNS and reverse proxying perform separate jobs: DNS locates Reese, while Caddy directs a web request to the correct service. MagicDNS improves tailnet device naming but does not replace service-level routing.

Backend ports remain necessary but no longer require routine public appearances. The colon was not malicious; the surrounding architecture had failed to provide it with privacy. Finch was justified in demanding names, and Root was instructed to stop treating arbitrary numbers as memorable.

## Committee Findings

### Transcript of the Addressing Inquiry

**Finch:** “Why does Grafana require a number?”

**Root:** “That number is its port. It tells the request which service endpoint to use.”

**Finch:** “Why does it tell me? I am trying to see a graph, not unload freight at Warehouse 6042.”

**An Unnamed Port:** “I have occupied this position for years. My work is essential.”

**A Colon:** “For the record, I merely separate the host from the port. I do not choose the number, advertise it, or enjoy being stared at.”

**DNS:** “I can direct `grafana.reese` to Reese. Once the visitor reaches Reese, my jurisdiction ends.”

**Reese:** “This is awkward. I contain rather a lot of offices.”

**Caddy:** “Give me the requested hostname and an approved route. I will send the visitor to the correct office without requiring them to memorise the loading bay.”

**Elias:** “I can transport authorised visitors securely to the property. Reception duties are outside my job description.”

**HR:** “I have submitted the Caddy configuration.”

**Caddy:** “You have submitted indentation anxiety and a syntax offence. Please try again after validation.”

**Finance Department:** “Do friendly names require a branding budget?”

**Root:** “The names are free. This meeting was not.”

**Finch:** “Good. Hide the ports.”

## Official Colon Crime Classification

### Class I — Minor Offence

A temporary troubleshooting address containing a port.

**Disposition:** Permitted under supervision.

### Class II — Repeat Offence

A bookmarked service address containing a port despite a friendly name being available.

**Disposition:** Bookmark rehabilitation required.

### Class III — Aggravated Colon Crime

Documentation instructing Future Daniel to remember several unexplained ports.

**Disposition:** Immediate rewriting.

### Class IV — Institutional Colon Crime

A dashboard linking to raw backend addresses across the entire homelab.

**Disposition:** Referral to Caddy and the Department of Friendly Names.

### Class V — Crimes Against Navigation

Asking Finch to remember which of several visually identical addresses opens Sonarr.

**Disposition:** No defence accepted.

## Final Verdict

### The colon was found:

- Standards compliant
- Technically innocent
- Visually implicated
- Frequently present at the scene
- Overexposed
- In need of a quieter backend role
- A victim of poor architectural boundaries
- Aesthetically guilty

### The ports were found:

- Necessary
- Functional
- Numerous
- Bad at branding
- Difficult to remember
- Entirely too visible
- Better suited to internal routing
- Sentenced to life behind Caddy

### DNS was found:

- Helpful
- Essential
- Good with addresses
- Unable to distinguish offices without assistance
- Not a reverse proxy
- Tired of being blamed for every browser problem

### Caddy was found:

- Polite
- Organised
- Capable of reading hostnames
- Qualified to operate the reception desk
- Responsible for directing visitors to the correct container
- Increasingly critical to daily navigation

### Elias was found:

- Secure
- Remote
- Excellent at transport
- Not parked outside
- Not employed as a receptionist

## Related Documentation

- [Operation Creepy Van Network](/Operations/Operation-creepy-van-network)
- [Network Map](/Infrastructure/Network-Map)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Elias / Tailscale Runbook](/Runbooks/Tailscale)
- Operation Reception Desk — dedicated operation page still to be created
