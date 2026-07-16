---
title: Operation Reception Desk
description: Document Caddy as the intended reverse proxy and front desk for friendly service-name requests reaching Reese.
published: true
date: 2026-07-16T00:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-07-16T00:00:00.000Z
---

# Operation Reception Desk

> **Status:** Active foundation completed, with refinement ongoing

> **Scope note:** This page documents a local and tailnet routing architecture. It does not establish public exposure, completed HTTPS configuration, or a live route for every proposed friendly name.

## Objective

Deploy and document a reverse-proxy layer that allows friendly service names to reach the correct applications on Reese without exposing backend ports in routine browser addresses.

Practical objectives:

- receive requests for friendly service names
- inspect the requested hostname
- send the request to the correct backend service
- keep backend ports hidden from normal users
- simplify bookmarks and documentation
- provide one consistent entry point
- support local access
- support remote access over Elias where DNS is available
- preserve direct backend access for troubleshooting
- document the routing architecture
- make Caddy configuration recoverable and maintainable

> “Finch should be able to ask for Grafana without presenting a socket coordinate.”

## Background

[Operation No More Colon Crimes](/Operations/Operation-no-more-colon-crimes) identified the usability problem. The homelab had multiple services, multiple ports, multiple bookmarks, multiple opportunities to type one number incorrectly, and no central receptionist.

DNS could resolve friendly names to Reese, but Reese contained many web services. Knowing the building address did not identify the office that should answer. The infrastructure needed neither fewer services nor a longer Book of Numbers. It needed someone at the front desk.

The Committee therefore authorised the hiring of Caddy as receptionist, switchboard operator, visitor-routing specialist, and keeper of the service directory. Caddy was the only candidate willing to read the hostname before answering, was increasingly overqualified for the number of visitors, and remained professionally unimpressed by raw port numbers.

The central question was:

> “How do we stop Finch arriving at Reese and shouting port numbers into the hallway?”

The core finding followed:

> DNS could locate the building. Elias could provide transport. Caddy had to run reception.

## Incident Classification

- **Incident type:** Visitor-routing failure
- **Location:** Reese front entrance
- **Victim:** Human navigation
- **Primary symptom:** “Connection refused” after Finch guessed the wrong number
- **Existing transport provider:** Elias
- **Existing address service:** DNS
- **Missing role:** Reception
- **Successful candidate:** Caddy
- **HR risk:** Caddyfile configuration
- **Committee priority:** High enough to justify another operation name

## Act I: Visitors Arrive at the Building

Before Caddy, a visitor could know Reese's address, reach Reese successfully, and still not know which application should answer. Reachability solved the journey, not the final destination.

The common experience was:

1. Finch opened a browser.
2. Finch entered a host and port.
3. Finch hoped the number was correct.
4. The intended service, the wrong service, or nothing answered.
5. DNS was briefly blamed.
6. Root explained that DNS was not involved in the mistake.
7. Finch became less interested in technical distinctions.

The infrastructure was reachable. It was not welcoming. Every application behaved like an upstairs department shouting its own extension into the lobby and expecting visitors to take notes.

## Act II: DNS Provides Directions

DNS resolves names to addresses. A suitable DNS layer can resolve `grafana.reese`, `library.reese`, and several other service names toward Reese. This reduces reliance on raw IP addresses and allows multiple useful names to identify the same application host.

DNS can:

- resolve `grafana.reese` to Reese
- resolve `library.reese` to Reese
- resolve several service names to the same Reese address
- reduce reliance on raw IP addresses

DNS cannot:

- know which backend application should answer an HTTP request
- map several hostnames to different Docker ports by itself
- operate as an HTTP reverse proxy
- infer the service from vibes
- prevent Finch from blaming it anyway

> “DNS delivered the visitor to the correct street address and considered the matter closed.”

The exact DNS implementation remains active or evolving. The target names are not treated as universally live until local and tailnet clients have been validated.

## Act III: Elias Provides Transport

Elias / Tailscale provides secure remote connectivity. It allows authorised clients to reach Reese from outside the LAN, MagicDNS assists with tailnet device names, and the design avoids requiring public port-forwarding crimes.

Elias can:

- provide secure remote connectivity
- allow Finch to reach Reese from outside the LAN
- help resolve tailnet device names through MagicDNS
- avoid public port forwarding

Elias cannot:

- route `grafana.reese` to Grafana by himself
- decide which container should answer
- operate the reception desk
- escort Finch through the building
- remember every service port out of professional courtesy

> “Elias got Finch onto the property. He refused to work reception.”

MagicDNS is helpful at the device-naming layer. It does not automatically create service-level hostname routes or replace Caddy.

## Act IV: Caddy Is Hired

Caddy receives HTTP requests and examines the requested hostname, commonly conveyed in the HTTP `Host` header. An approved hostname rule can then forward the request to the correct reachable backend service and port, after which Caddy returns the backend response to the client.

Conceptually:

- a request for `grafana.reese` can be routed to Grafana
- a request for `library.reese` can be routed to Wiki.js
- a request for `sonarr.reese` can be routed to Sonarr
- a request for `seer.reese` can be routed to Seerr

These are intended mappings, not assertions that every route is currently live. Exact backend ports and Caddyfile entries are deliberately omitted.

Caddy's job is to:

- listen for incoming requests
- inspect the requested hostname
- match the friendly service name
- forward the request to the correct backend
- return the response
- conceal backend implementation details
- keep the hallway quiet

### Candidate Interview

**Root:** “Can you read hostnames?”

**Caddy:** “Yes.”

**Root:** “Will you forward requests, work with container backends, remain calm during DNS accusations, and avoid asking Finch to memorise ports?”

**Caddy:** “Provide valid configuration and reachable backends.”

**HR:** “Are you prepared to work with configuration documents?”

**Caddy:** “Valid ones.”

**Committee:** “Do you object to being called Reception Desk?”

**Caddy:** “I have seen your container names. This is fine.”

Caddy was hired immediately. Finance later clarified that “hired” carried no salary implications.

## Act V: The Front Desk Directory

The conceptual directory is:

| Visitor asks for | DNS sends visitor to | Caddy routes to | Department |
| --- | --- | --- | --- |
| `library.reese` | Reese | Wiki.js backend | Institutional memory |
| `grafana.reese` | Reese | Grafana backend | Pretty panic |
| `sonarr.reese` | Reese | Sonarr backend | Television acquisition |
| `seer.reese` | Reese | Seerr backend | Request desk |

> Backend ports are omitted because the receptionist handles internal extensions and because raw port numbers are currently in rehabilitation.

The directory records the intended logical relationship. A mapping becomes operational only after its DNS, Caddy route, backend reachability, and client path have been tested.

## Act VI: HR Produces the Caddyfile

The Caddyfile is the front desk's routing paperwork. Each hostname needs a correct route to a backend service. The hostname must agree with DNS, the backend must be reachable from Caddy, and the chosen Docker or host networking path must be understood.

Operational principles:

- each hostname requires a route
- each route points to a backend service and port
- syntax must be valid
- configured hostnames must match the intended DNS names
- backend services must be reachable from Caddy
- container networking or host networking must be understood
- configuration must be backed up
- configuration should be validated before reload
- logs should be checked after changes
- one typo can send visitors to the wrong office or no office at all

Safe generic checks include:

```bash
caddy validate --config <path-to-Caddyfile>
docker logs --tail=100 <caddy-container>
curl -I http://<friendly-name>
```

The placeholders must be replaced with verified local values. This page does not assert an actual Caddyfile path or container name.

HR submitted invalid syntax in triplicate, filed one hostname under the wrong department, and omitted the backend extension from another form. Root called the result “almost self-documenting.” Finch observed that punctuation had returned through another door and requested that validation occur before the building opened.

## Act VII: Opening Day

The intended opening-day test is deliberately ordinary:

1. A friendly name resolves.
2. The request reaches Reese.
3. Caddy reads the hostname.
4. Caddy forwards the request to the correct backend.
5. The service opens.
6. The backend port remains unseen by the visitor.
7. Finch experiences an address containing actual words.
8. Root immediately proposes adding more services.

> “The service opened without Finch consulting the Book of Numbers.”

This is the active validation model. The repository does not yet provide enough evidence to name a particular route as fully validated across LAN and tailnet clients, so the Committee has not fabricated an opening-day success report merely because the ribbon was already ordered.

## Technical Architecture

```text
Local or remote client
  → DNS resolution
  → Reese
  → Caddy
  → selected backend service
```

For remote access:

```text
Remote client
  → Elias / Tailscale
  → DNS available to client
  → Reese
  → Caddy
  → selected backend
```

- DNS determines where Reese is.
- Elias provides secure remote reachability.
- Caddy decides which service receives the HTTP request.
- Docker or the host provides backend connectivity.
- The browser uses the friendly service name and need not expose the backend port.

Caddy does not replace DNS, and neither Caddy nor MagicDNS makes public exposure necessary.

## Systems Involved

- Reese
- Ubuntu Server
- Docker
- Caddy
- DNS
- Elias / Tailscale
- MagicDNS
- Wiki.js / The Library
- Grafana
- Sonarr
- Seerr
- Zoe / Homepage
- Shaw / Portainer
- Carter / Uptime Kuma
- browser clients
- bookmarks
- HR / Caddyfile configuration
- Committee Department of Visitor Services

## Technical Risks Considered

These are considered risks, not a claim that every one occurred:

- DNS points to the wrong Reese address
- Caddy route points to the wrong backend
- backend port is incorrect
- backend service is unavailable
- Caddy cannot reach the container network
- hostname mismatch
- browser cache
- stale DNS
- HTTP/HTTPS confusion
- certificate expectations
- local access works but remote access does not
- remote DNS differs from LAN DNS
- Reese uses a different address after Ethernet failure
- Caddy becomes a single point of navigation failure
- direct backend route is undocumented
- configuration changes are not backed up
- HR commits syntax crimes
- every failure is blamed on DNS before logs are checked

## Actions Taken or Planned

Repository evidence confirms the naming and routing architecture, secure remote transport, MagicDNS device naming, and the need for a Caddy reception layer. It does not confirm a completed Caddy deployment or every route and validation.

| Step | Action | Status |
| --- | --- | --- |
| 1 | Select friendly service names | Foundation completed; expansion active |
| 2 | Ensure DNS resolves names toward Reese | Active / final implementation evolving |
| 3 | Deploy or identify Caddy as reverse proxy | Selected; deployment not confirmed here |
| 4 | Define hostname-to-backend routes | Active / planned |
| 5 | Validate configuration | Planned per change |
| 6 | Start or reload Caddy | Planned; completion not claimed |
| 7 | Test each friendly name | Planned per route |
| 8 | Test locally | Planned |
| 9 | Test over Elias / Tailscale | Planned |
| 10 | Retain direct backend access | Rollout and troubleshooting policy |
| 11 | Update bookmarks | Planned after validation |
| 12 | Update Zoe / Homepage links | Planned after validation |
| 13 | Update The Library documentation | Active; architecture documented here |
| 14 | Back up Caddy configuration | Planned |
| 15 | Document recovery and bypass procedures | Planned |
| 16 | Investigate wired/Wi-Fi power-cut resilience | Active follow-on concern |

## Validation

Validation for each route should establish that:

- the hostname resolves to Reese
- Caddy receives the request
- the correct backend responds
- the wrong backend does not respond
- the service loads through the friendly address
- direct backend access remains available for troubleshooting
- local and remote paths are checked separately
- logs contain no routing errors
- browser cache is ruled out during inconsistent tests
- Caddy restarts successfully after configuration changes
- configuration survives reboot where applicable

Confirmed today: Reese hosts the relevant applications, Elias provides secure remote access, and MagicDNS resolves tailnet device names. Per-route Caddy reception, LAN DNS, tailnet DNS, restart, and reboot validation remain unconfirmed by the available documentation.

## Outcome

- Caddy was selected as the front desk; deployment status requires implementation evidence
- service routing gained a central documented architecture
- backend ports became internal extensions in the preferred design
- friendly names became the preferred human-facing access method
- DNS, Elias, and Caddy gained clearly separated responsibilities
- direct port access remained available for troubleshooting
- The Library documented the routing model
- refinement and resilience work remained ongoing
- the homelab acquired a receptionist despite having no payroll department

## Mission Status

**ACTIVE FOUNDATION COMPLETED — RECEPTION REMAINS STAFFED**

> The front desk is considered critical infrastructure. Direct backend access remains the emergency side entrance.

## Help Guide

# How to Operate a Building With No Receptionist

### Step 1: Build many offices

Deploy containers for monitoring, media automation, documentation, requests, and administration.

### Step 2: Give each office an extension

Use backend ports.

### Step 3: Publish the extensions as public directions

Expect Finch to remember them.

### Step 4: Add DNS

Direct everyone to the building.

### Step 5: Provide no directory

Allow visitors to wander the halls shouting numbers.

### Step 6: Blame DNS when they enter the wrong office

Repeat until morale improves.

### Step 7: Hire Caddy

Place one competent person at the front desk.

### Step 8: Replace extensions with names

Allow Finch to ask for Grafana like a civilised person.

### Step 9: Document the emergency side entrance

Keep direct backend routes for troubleshooting.

## Front Desk Service Standards

- Visitors will be greeted by hostname.
- Visitors will not be asked to remember backend ports.
- DNS complaints will be redirected to the correct department.
- Elias will not be assigned reception duties.
- Backend services must answer internal calls.
- HR must validate the Caddyfile before opening.
- Raw port numbers may be disclosed during emergencies only.
- Root may not add a new route without documenting it.
- Finch may use interpretive swearing during outages but must still check logs.

## Coffee Status

- Caddy research: One cup
- DNS explanation: Cup reheated
- First route: Fresh cup authorised
- First configuration typo: Coffee placed down carefully
- Friendly service opens: Victory coffee
- Root proposes routing every service immediately: Coffee confiscated by Health & Safety

## Casualties

- several raw bookmarks
- backend ports removed from public-facing duty
- one imaginary reception bell
- Elias's attempt to leave before being assigned more work
- DNS's remaining patience
- HR's confidence in punctuation
- Root's habit of shouting port numbers down the hallway
- no services
- no containers
- no visitors permanently lost
- no actual receptionist salary

## Lessons Learned

### Practical Lessons

- DNS and reverse proxying solve different problems.
- Tailscale provides reachability, not service routing.
- Friendly names require consistent DNS.
- Caddy routes by hostname.
- Backend connectivity must be tested.
- Retain direct access for troubleshooting.
- Validate configuration before reload.
- Back up reverse-proxy configuration.
- Test LAN and tailnet clients separately.
- Document every route.
- Reverse proxies become critical infrastructure.
- Check logs before blaming DNS.
- Power-cut address changes require resilience planning.

### Committee Lessons

- Locating the building is not the same as finding the office.
- Every homelab eventually hires a receptionist.
- Ports are internal extensions and should behave accordingly.
- Elias is transport and has repeatedly declined customer-service duties.
- DNS is not responsible for escorting visitors.
- Caddy is the only component paid entirely in configuration files.
- HR can break the front desk with one misplaced character.
- Finch should never again have to ask which number is Grafana.
- Root will use any routing success as justification for adding another route.
- A browser address containing words is an infrastructure achievement.
- The emergency side entrance should remain available but undisclosed to ordinary guests.

## Official Findings

The Committee finds that the homelab was reachable but lacked visitor routing. DNS located Reese and Elias provided secure transport; neither performed service-level reception. Caddy filled the missing architectural role by reading hostnames and routing requests toward the intended backends.

Friendly names improve usability. Backend ports remain necessary but become internal extensions. Direct backend access remains valuable for troubleshooting. The Caddyfile requires validation, backup, and recovery documentation. Finch was justified in demanding a front desk, Root was instructed to stop treating port numbers as a hospitality strategy, and no actual receptionist was hired because Finance denied the position.

## Committee Findings

### Front Desk Meeting Transcript

**Finch:** “I am here for Grafana.”

**DNS:** “Reese is at the expected address. My work is complete.”

**Elias:** “Transport is also complete. Finch is securely on the property.”

**Finch:** “Excellent. Where is Grafana inside Reese?”

**Reese:** “There are several departments upstairs, and all of them believe their extension is memorable.”

**Grafana, from upstairs:** “Pretty panic department! Internal extension withheld!”

**Wiki.js / The Library:** “Visitors keep opening my door while looking for dashboards. It is disrupting institutional memory.”

**Caddy:** “If the visitor asks for `grafana.reese`, I can direct the request to Grafana. If they ask for `library.reese`, I can send them to The Library.”

**HR:** “Here is the routing form.”

**Caddy:** “This hostname is malformed, the backend is missing, and the syntax has been signed in the margin.”

**Root:** “The configuration is elegant once you understand it.”

**Finch:** “That is what you said about the ports.”

**Finance Department:** “Does the receptionist expect wages?”

**Caddy:** “I accept valid configuration.”

**Finance Department:** “Approved.”

**Health & Safety:** “No running in the hallway during outages. Check the logs and proceed calmly.”

## Official Departmental Responsibilities

### DNS

**Role:** Address directory

**Responsible for:** Resolving service names toward Reese

**Not responsible for:** Selecting the backend application

### Elias

**Role:** Secure transport

**Responsible for:** Remote reachability

**Not responsible for:** Reception, office navigation, or remembering ports

### Caddy

**Role:** Reception and switchboard

**Responsible for:** Reading hostnames and routing visitors to the correct backend

**Not responsible for:** Fixing a backend service that is already dead

### Docker

**Role:** Office tenancy management

**Responsible for:** Running the services

**Not responsible for:** Providing friendly public directions

### HR

**Role:** Configuration paperwork

**Responsible for:** Submitting valid Caddyfile changes

**Frequently investigated for:** Syntax crimes

### Finch

**Role:** Visitor and operator

**Responsible for:** Asking for services by name

**No longer responsible for:** Remembering arbitrary internal extensions

## Final Verdict

### Caddy was found:

- Polite
- Capable
- Hostname literate
- Calm under pressure
- Qualified to run reception
- Willing to route visitors
- Increasingly critical
- The only component that asked who Finch was there to see

### DNS was found:

- Accurate
- Useful
- Good with buildings
- Not an office directory
- Frequently blamed outside its remit
- Entitled to refer complaints to reception

### Elias was found:

- Secure
- Efficient
- Excellent at transport
- Unwilling to work the front desk
- Not parked outside
- Cleared of all reception-related duties

### The backend ports were found:

- Necessary
- Internal
- Poor conversationalists
- Better suited to extension numbers
- No longer allowed to greet visitors directly
- Available through the emergency side entrance

### Root was found:

- Correct about the architecture
- Excessively excited by reverse proxying
- In possession of a proposed route for every service
- Required to document before expanding
- Still trying to give Caddy a uniform

### Finch was found:

- Correct
- Entitled to readable service names
- No longer wandering the hallway in the intended architecture
- In possession of cleaner bookmarks once routes are validated
- Responsible for hiring the first fictional employee in the homelab

## Best Quotes

> “DNS knew where the building was. Caddy knew which office Finch wanted.”

> “The homelab did not need fewer services. It needed someone at the front desk.”

> “Ports are internal extensions. Stop making visitors dial them from the car park.”

## Follow-On Operations

- [Operation No More Colon Crimes](/Operations/Operation-no-more-colon-crimes)
- [Operation Creepy Van Network](/Operations/Operation-creepy-van-network)
- Operation DNS Shenanigans — dedicated page still required
- power-cut DNS resilience for `grafana.reese`
- Caddy configuration backup
- Zoe / Homepage link updates
- service catalogue updates
- friendly-name testing over Elias
- direct-backend troubleshooting documentation
- future HTTPS or certificate planning where appropriate
- reverse-proxy monitoring
- potential second Reese address handling during Ethernet failure

## Series Status

The operation was commissioned as a corporate-transformation series. The pilot featured DNS directing everyone to the same building, Elias dropping remote visitors at the gate, and the containers shouting extension numbers from upstairs.

Caddy arrived, opened the directory, and explained the entire architecture before the opening credits finished. Root immediately proposed a route for every service, a brass reception bell, and an after-hours escalation rota. Health & Safety rejected the bell as an outage distraction.

The network attempted to renew the programme as **Reception Desk: After Hours**. The Committee approved a limited series because Root had already drafted several more episode titles. Finance declined the fictional receptionist's salary request. Caddy requested valid configuration instead and continued working anyway—or will do so as each route is deployed and validated, which Legal insisted was less cinematic but more accurate.

## Related Documentation

- [Operation No More Colon Crimes](/Operations/Operation-no-more-colon-crimes)
- [Operation Creepy Van Network](/Operations/Operation-creepy-van-network)
- [Network Map](/Infrastructure/Network-Map)
- [Service Catalogue](/Infrastructure/Service-Catalogue)
- [Elias / Tailscale Runbook](/Runbooks/Tailscale)
- [Operation Archive](/Operations/Operation-Archive)
- [Recovered Operations Inbox](/Operations/Recovered-Operations-Inbox)
- [Library Status](/Library-Status)
- [Canon](/Canon)
