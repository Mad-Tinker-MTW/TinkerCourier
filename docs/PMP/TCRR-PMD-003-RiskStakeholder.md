# Risk and Stakeholder Register
**TinkerCourier**
Document ID: TCRR-PMD-003
Version: 1.0
Date: 2026-06-14
Project Manager: Francisco De La Paz

---

## Risk Register

| ID | Risk | Likelihood | Impact | Level | Mitigation |
|---|---|---|---|---|---|
| R-01 | Windows credential vault not accessible from a Scheduled Task without an interactive logon | Medium | High | High | Install task under the logged-in user with "Run only when user is logged on"; document the LocalSystem trap; fall back to interactive console as the supported runtime |
| R-02 | GitHub rate limits or push throttling on a poll-heavy daemon | Low | Medium | Low | Default poll interval at 60s; use authenticated SSH (higher limits than anonymous); add jitter; webhook trigger in Stage 2 |
| R-03 | Payload schema drift between phone clients and daemon | Medium | Medium | Medium | Version every payload; reject unknown versions with a structured error receipt; document the schema in SPEC |
| R-04 | Single-PC dependency: dispatch stops if the host is offline | Medium | Medium | Medium | Daemon resumes from the last committed receipt on restart; payloads pile up safely in the repo while host is offline |
| R-05 | Attachment path semantics differ across client devices (phone references files the host cannot see) | Medium | Medium | Medium | Restrict phone-originated payloads to attachments already committed in the repo; allow absolute host paths only for trusted local origins |
| R-06 | Secret leakage if a client tries to put credentials in a payload | Low | High | Medium | Schema rejects fields that look like credentials; documentation warns; payloads are reference-only |
| R-07 | Replay attacks: same payload pushed twice double-sends | Medium | Medium | Low | Idempotency by request_id and content hash; receipts written before next dispatch |
| R-08 | TinkerWire upstream changes break SMTP transport | Medium | Medium | Medium | Pin TinkerWire version; integration tests on every TinkerWire upgrade |

---

## Stakeholder Register

| Name | Role | Power | Interest | Engagement |
|---|---|---|---|---|
| Francisco De La Paz | Project Sponsor, Project Manager, Solutions Architect, Lead Developer, End User, QA Engineer, Deployment Engineer | High | High | Drives every decision |
| Mad Tinker's Workshop | Primary validation environment | High | High | Daily dispatch friction is the operational driver |
| TinkerWire | Upstream SMTP module | Medium | High | Reused as the email transport; do not reimplement |
| MessageBurst | Downstream client (Stage 4) | Medium | High | BRST and email routes will dispatch through Courier |
| HexVeridicae | Downstream client (Stage 4) | Medium | Medium | Voice-triggered sends ride Courier |
| TinkerOps (Workshop Dev Console) | Observer | Low | Medium | Surfaces Courier health and receipt counts |
| 4Kings Enterprises | Parent organization | High | Medium | Tools-division product portfolio |
