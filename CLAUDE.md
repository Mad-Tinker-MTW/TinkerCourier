# TinkerCourier — Claude Code Context

## What This Is
A small Python daemon that watches a private GitHub repo for structured dispatch payloads (email, SMS, etc.), reads transport credentials from the local OS keyring, delivers the message through the appropriate provider, and commits a delivery receipt back. The transport layer is reused from TinkerWire where possible; TinkerCourier is the dispatcher, not the mailer.

## Stack
Python + uv + keyring (Windows Credential Manager) + git CLI (or GitPython) + smtplib via TinkerWire's mailer module. Local-only. No cloud hosting.

## Launch
`start.ps1` — runs the daemon in the foreground for development, or installs as a Scheduled Task for unattended operation.

## Project Rules
- Reuse TinkerWire's mailer for SMTP. Do not reimplement keyring or SMTP plumbing.
- Daemon must run under an interactive logon session so it can read the keyring. SSH sessions and LocalSystem cannot. Use a Scheduled Task that runs as the logged-in user, or run it from a local console.
- Every delivered payload must produce a signed receipt commit so the audit trail is complete.
- No secrets in payloads. Only references (recipient, subject, body, attachment paths). Credentials stay on the unlocked PC.
- Payload schema is versioned. Reject unknown versions rather than guess.

## Current Status
Scaffolded 2026-06-14. Ready for first build session.
