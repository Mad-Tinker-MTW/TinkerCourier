# TinkerCourier — Vision

## The Problem
Authenticated send is increasingly stuck behind credential vaults that only an interactive desktop session can unlock. Phones, SSH terminals, scheduled jobs, and remote agents are all on the wrong side of that wall. The result is a daily friction tax: simple things (send this PDF, ping this contact, post this update) require the operator to physically be at the unlocked PC or to keep app passwords scattered across devices.

## The Product
TinkerCourier is a small daemon that turns a private git repo into a dispatch queue. Any device that can push to the repo (which means anything with an SSH key) can request a delivery. The daemon, running on the unlocked PC, reads its local keyring, performs the send, and writes a signed delivery receipt back to the repo. Phones gain real send. Scheduled tasks gain real send. SSH gains real send. The operator gains an audit trail and a single place where credentials live.

## Origin
TinkerCourier was discovered, not designed. During a long resume-and-CV session, the operator was SSH'd into the workshop PC. The natural follow-up — email these PDFs through TinkerWire's SMTP — failed because Windows refused to release the keyring to a non-interactive logon session. As a workaround we created a private repo, committed the bundle, and pushed it; from any second device the PDFs could then be retrieved and sent. Mid-push, the operator asked whether that pattern was actually a clever way to send mail. It is. TinkerCourier formalizes the workaround into a reusable service.

## Principles
- Credentials stay on the authoritative PC. Payloads travel; secrets do not.
- Every delivery produces a receipt. The repo history is the audit log.
- Transports are pluggable. Email first, then SMS, then chat.
- Reuse, never reimplement. TinkerWire owns SMTP. TinkerCourier dispatches.
- Local-first. No cloud broker, no third-party queue.
- Idempotent by request_id. Re-pushing the same payload never double-sends.
