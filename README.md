# TinkerCourier
**Git-as-courier daemon that turns the SSH credential gap into a feature.**
Status: pre-build, 0.1.0
Last updated: 2026-06-14

Phones, laptops, and SSH sessions can't reach the local Windows Credential Manager, so they can't send authenticated email or SMS from your authoritative PC. TinkerCourier closes that gap. Any device pushes a structured payload into a private GitHub repo. A daemon on the unlocked PC polls the repo, reads the local keyring, delivers the message through the right transport (SMTP first, SMS and chat later), and commits a delivery receipt back. The result is a portable, audited dispatch layer for the whole MTW ecosystem.

Running locally at Q:\MTW\TinkerCourier on TINKERSWORKSHOP.
Repo: Mad-Tinker-MTW/TinkerCourier (pending)
Live: start.ps1 → background daemon (no public URL)

## Quick State
Pre-build. Scaffolded 2026-06-14. Not yet implemented.

## Context
TinkerCourier is a Tools-division daemon and a sibling to TinkerWire (which owns the SMTP credentials) and HexVeridicae (which is phone-reachable). It does not replace either; it routes work into them. The first delivered payload type is "send email with attachments," validated against the very use case that spawned the project: pushing resume PDFs through a private repo when the SSH session into the PC could not access the keyring directly.
