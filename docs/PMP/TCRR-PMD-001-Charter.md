# Project Charter
**TinkerCourier**
Document ID: TCRR-PMD-001
Version: 1.0
Date: 2026-06-14
Project Manager: Francisco De La Paz

---

## Project Overview

TinkerCourier is a Tools-division daemon developed under 4Kings Enterprises that turns a private GitHub repository into a dispatch queue for locally-authenticated transports. A small Python service running on the authoritative PC polls the repo, validates structured payloads, and delivers each message through the right transport (SMTP first via TinkerWire, then SMS, then chat). Every delivery produces a receipt commit so the repo history is the audit log.

The project is developed and validated at Mad Tinker's Workshop, where it removes a recurring friction: phones, SSH sessions, and scheduled jobs cannot reach the Windows Credential Manager and therefore cannot send authenticated email or SMS directly. TinkerCourier closes that gap by letting any device push a payload while credentials stay on the unlocked PC.

---

## Business Need

A growing share of MTW operations are triggered from devices that cannot reach the local keyring. Sending a resume from an SSH session, dispatching a TinkerWire post from a phone, or having a scheduled task email a daily report all fail at the same point: Windows refuses to release the credential vault to a non-interactive session. The current workaround is to be physically at the unlocked PC or to scatter app passwords across devices. TinkerCourier replaces that workaround with a small reusable service that already proved itself once (the resume-bundle push that spawned it) and generalizes the pattern into a real product.

---

## Objectives

1. Deliver Stage 1 minimum courier: payload schema v1, repo polling, SMTP dispatch via TinkerWire, delivery receipts
2. Add hardening and Scheduled Task deployment in Stage 2 so the daemon runs unattended
3. Extend the transport set in Stage 3 (SMS, Discord, Slack) so the same dispatch flow covers all common channels
4. Integrate with TinkerWire, MessageBurst, and HexVeridicae in Stage 4 so the broader ecosystem can dispatch through Courier rather than re-implement send

---

## Scope

### In Scope
- Private GitHub repo as the dispatch queue
- Payload schema (versioned) and validation
- Repo poller with content-hash idempotency
- Dispatcher routing on payload type
- SMTP transport that delegates to TinkerWire's mailer
- Delivery receipt commits back to the repo
- Local rotating audit log on the host
- Scheduled Task installer for unattended operation
- SMS, Discord, and Slack transports (Stage 3)
- Compose handoffs from TinkerWire, MessageBurst, and HexVeridicae (Stage 4)

### Out of Scope
- Cloud-hosted dispatch broker (local-only by design)
- Multi-tenant operation (one PC owns the keyring)
- Secret transport in payloads (credentials never travel)
- Real-time chat or two-way conversations (this is dispatch, not chat)
- General-purpose CI/CD runner

---

## Deliverables

| Deliverable | Target Date |
|---|---|
| Stage 1: Minimum Courier (email via TinkerWire) | TBD |
| Stage 2: Hardening and Scheduled Task | TBD |
| Stage 3: Reach (SMS, Discord, Slack) | TBD |
| Stage 4: Ecosystem Integration (TinkerWire, MessageBurst, HexVeridicae) | TBD |

---

## Milestones

| Milestone | Date |
|---|---|
| Project scaffolded | 2026-06-14 |
| First delivered email payload | TBD Stage 1 |
| Daemon running as Scheduled Task | TBD Stage 2 |
| First SMS or chat payload delivered | TBD Stage 3 |
| First payload originating in another MTW module | TBD Stage 4 |

---

## Budget Summary

| Category | Amount |
|---|---|
| Labor, Stage 1 (28 hrs at $85/hr) | $2,380 |
| Labor, Stage 2 (16 hrs at $85/hr) | $1,360 |
| Labor, Stage 3 (24 hrs at $85/hr) | $2,040 |
| Labor, Stage 4 (20 hrs at $85/hr) | $1,700 |
| Tools and hosting | < $50 |
| **Total** | **~$7,530** |

---

## Stakeholders

| Name | Role | Interest |
|---|---|---|
| Francisco De La Paz | Project Sponsor, Project Manager, Solutions Architect, Lead Developer, End User, QA Engineer, Deployment Engineer | Full ownership |
| Mad Tinker's Workshop | Primary validation environment | Daily dispatch friction removed |
| TinkerWire | Upstream SMTP module | Reused by Courier, not duplicated |
| MessageBurst | Future client | Routes BRST sends through Courier |
| HexVeridicae | Future client | Voice-triggered sends ride Courier |
| 4Kings Enterprises | Parent organization | Tools-division product portfolio |

---

## Risks (Summary)

| Risk | Level |
|---|---|
| Windows credential vault not accessible from Scheduled Task without interactive context | High |
| GitHub rate limits on poll-heavy workloads | Low |
| Payload schema drift between client devices and daemon | Medium |
| Single-PC dependency: dispatch stops if the host is offline | Medium |
| Attachment path semantics differ across client devices | Medium |

---

## Authorization

Project authorized under 4Kings Enterprises Tools-division development.
Project Manager: Francisco De La Paz
Date: 2026-06-14
