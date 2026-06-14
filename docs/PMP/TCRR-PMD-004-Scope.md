# Scope Statement
**TinkerCourier**
Document ID: TCRR-PMD-004
Version: 1.0
Date: 2026-06-14
Project Manager: Francisco De La Paz

---

## Product Scope Description

TinkerCourier is a single-tenant, local-only Python daemon that consumes structured dispatch payloads from a private GitHub repository and delivers them through locally-authenticated transports. The daemon runs on the operator's authoritative PC under an interactive logon session so it can read the Windows Credential Manager. It exposes no public network surface. Its inputs are payload files committed to the repo; its outputs are real deliveries (email, SMS, chat) and receipt files committed back. The product is a dispatcher, not a transport: each transport handler delegates to an existing MTW module (TinkerWire's mailer first; future SMS and chat modules later) so credentials and provider logic stay where they already live.

---

## Project Deliverables

1. Stage 1: a working Python package with payload schema v1, repo poller, SMTP dispatch via TinkerWire, receipt commits, console runner, and a smoke-test replay of the resume-bundle scenario.
2. Stage 2: a Scheduled Task installer, structured logging, retry-and-backoff failure handling, local audit log, dry-run mode, and TOML config file.
3. Stage 3: payload schema v2, SMS transport (Twilio or self-hosted), Discord and Slack webhook transports, repo-based address book, and per-transport routing rules.
4. Stage 4: TinkerWire, MessageBurst, and HexVeridicae integration; a phone client (Working Copy template and Termux script); a cross-module audit view in TinkerOps.

---

## Acceptance Criteria

- A payload committed to the dispatch repo is delivered through the correct transport within the configured poll interval plus transport time.
- Every delivery produces a receipt commit visible in the repo history.
- The daemon refuses any payload whose schema version it does not recognize, and writes a structured error receipt instead of silently failing.
- Re-pushing the same payload by request_id never produces a second delivery.
- TinkerWire's mailer is the only path for SMTP; TinkerCourier does not bundle SMTP credentials.

---

## Constraints

- Daemon must run under an interactive user logon to access the keyring; LocalSystem and SSH sessions cannot.
- Local-only operation; no cloud broker, no third-party queue, no hosted relay.
- Single-tenant; one PC owns the keyring, one daemon dispatches.
- Reuse of TinkerWire's mailer is mandatory for email; reimplementation is out of scope.
- No secrets in payloads. Payloads carry references and recipient addresses, not credentials.

---

## Assumptions

- The operator's PC is generally on and logged in when payloads are pushed.
- SSH-key authentication to GitHub is in place for both the daemon and the client devices.
- TinkerWire's mailer module and its keyring entries remain the authoritative SMTP path on the host.
- Phone clients can push to the private repo via Working Copy, Termux, or equivalent.
- Payload volume stays in the low tens per day for the foreseeable future, so polling at 60s is adequate without a webhook in Stage 1.

---

## Exclusions

- No cloud-hosted dispatch broker.
- No multi-tenant or team operation in the initial product lifecycle.
- No two-way conversational messaging (this is dispatch, not chat).
- No general-purpose CI/CD runner or code execution beyond dispatch.
- No public API surface or external authentication layer; access is gated by GitHub repo permissions.
