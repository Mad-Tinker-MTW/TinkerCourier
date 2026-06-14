# Work Breakdown Structure
**TinkerCourier**
Document ID: TCRR-PMD-002
Version: 1.0
Date: 2026-06-14
Project Manager: Francisco De La Paz

---

#### 1.1 Stage 1: Minimum Courier

| ID | Task | Status |
|---|---|---|
| 1.1.1 | Python + uv scaffold, package layout, entry point | Pending |
| 1.1.2 | Payload schema v1 definition and JSON schema validator | Pending |
| 1.1.3 | Repo poller: clone, fetch loop, configurable interval | Pending |
| 1.1.4 | Outbox walker: discover new payloads, content-hash idempotency | Pending |
| 1.1.5 | Dispatcher: route on payload.type | Pending |
| 1.1.6 | SMTP transport: delegate to TinkerWire mailer with attachments | Pending |
| 1.1.7 | Receipt writer: build receipt JSON, commit, push | Pending |
| 1.1.8 | Local console runner with verbose logging | Pending |
| 1.1.9 | End-to-end smoke test: resume-bundle replay | Pending |
| 1.1.10 | Stage 1 documentation and CHANGELOG update | Pending |

---

#### 1.2 Stage 2: Hardening and Operations

| ID | Task | Status |
|---|---|---|
| 1.2.1 | Scheduled Task installer script (runs as logged-in user) | Pending |
| 1.2.2 | Structured logging with file rotation | Pending |
| 1.2.3 | Failure handling: classify transient vs terminal, retry backoff | Pending |
| 1.2.4 | Local audit log alongside repo receipts | Pending |
| 1.2.5 | Dry-run mode: validate and report, do not send | Pending |
| 1.2.6 | Health endpoint or heartbeat receipt | Pending |
| 1.2.7 | Config file (TOML) for poll interval, repo URL, log level | Pending |
| 1.2.8 | Stage 2 validation and CHANGELOG update | Pending |

---

#### 1.3 Stage 3: Reach (additional transports)

| ID | Task | Status |
|---|---|---|
| 1.3.1 | Payload schema v2: type tag set widened, transport hints | Pending |
| 1.3.2 | SMS transport: provider abstraction (Twilio or self-hosted gateway) | Pending |
| 1.3.3 | Discord webhook transport | Pending |
| 1.3.4 | Slack webhook transport | Pending |
| 1.3.5 | Address book in the repo: alias to recipient resolution | Pending |
| 1.3.6 | Per-transport routing rules (priority, fallback) | Pending |
| 1.3.7 | Stage 3 validation and CHANGELOG update | Pending |

---

#### 1.4 Stage 4: Ecosystem Integration

| ID | Task | Status |
|---|---|---|
| 1.4.1 | TinkerWire compose handoff: publish a wire as a Courier payload | Pending |
| 1.4.2 | MessageBurst route: BRST sender pushes payload, Courier delivers | Pending |
| 1.4.3 | HexVeridicae voice trigger: Angie composes, Courier carries | Pending |
| 1.4.4 | Phone client: Working Copy template and Termux script for payload push | Pending |
| 1.4.5 | Cross-module audit dashboard: list receipts by origin module | Pending |
| 1.4.6 | Stage 4 validation and full documentation update | Pending |

---

#### 1.5 Project Management (ongoing)

| ID | Task | Status |
|---|---|---|
| 1.5.1 | Maintain BUGS.md | Ongoing |
| 1.5.2 | Maintain CHANGELOG.md | Ongoing |
| 1.5.3 | Update ROADMAP.md checkboxes per stage | Ongoing |
| 1.5.4 | Obsidian journal entries per session | Ongoing |
| 1.5.5 | GitHub commits per session | Ongoing |
| 1.5.6 | PMP updates at stage gates | Ongoing |

---

## Actual Hours Log

| Date | Role | Hours | Notes |
|---|---|---|---|
| 2026-06-14 | Project Manager | 2.0 | Scaffold session: intake, structure, docs, PMP, registry |
