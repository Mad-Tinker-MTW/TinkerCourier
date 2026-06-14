# TinkerCourier — Roadmap

## Stage 1: Minimum Courier (current)
- [ ] Payload schema v1: email with attachments
- [ ] Repo poller loop with content-hash idempotency
- [ ] Dispatcher routing on payload type
- [ ] SMTP delivery via TinkerWire mailer
- [ ] Delivery receipt commit back to repo
- [ ] Local console runner

## Stage 2: Hardening and Operations
- [ ] Scheduled Task installer for unattended operation
- [ ] Structured logging with rotation
- [ ] Failure handling and retry backoff
- [ ] Local audit log alongside repo receipts
- [ ] Dry-run mode

## Stage 3: Reach (additional transports)
- [ ] SMS provider integration (Twilio or self-hosted gateway)
- [ ] Discord and Slack webhook transports
- [ ] Per-transport routing rules
- [ ] Recipient address book in the repo

## Stage 4: Ecosystem Integration
- [ ] TinkerWire compose handoff: dispatch a wire post as a payload
- [ ] MessageBurst route: BRST sender, courier delivers
- [ ] HexVeridicae voice trigger: ask Angie to send something, courier carries it
- [ ] Phone client (Working Copy template or Termux script) to push payloads
