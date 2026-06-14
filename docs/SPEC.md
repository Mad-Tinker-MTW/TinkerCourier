# TinkerCourier — Specification

## What It Is
A polling daemon that consumes structured dispatch payloads from a private GitHub repo and delivers them through locally-authenticated transports. It exists because OS keyrings are only available to interactive logon sessions on the authoritative PC, while many useful trigger contexts (phones, SSH sessions, laptops away from home) cannot reach that keyring. TinkerCourier inverts the flow: the payload travels, the credentials stay.

## Stack
| Layer | Tech |
|---|---|
| Language | Python 3.12+ |
| Package manager | uv |
| Secret store | OS keyring (Windows Credential Manager) via the `keyring` library |
| Repo access | git CLI (preferred) or GitPython |
| Email transport | smtplib via TinkerWire's `mailer` module |
| Future transports | SMS (Twilio or self-hosted), Discord/Slack webhooks |
| Runtime | Local-only, Scheduled Task or interactive console |

## Architecture
1. **Repo poller**: clones the dispatch repo, fetches on an interval (default 60s) or on a webhook trigger.
2. **Payload reader**: walks the `outbox/` folder, parses any new `*.json` payloads, validates against the schema for that version, and content-hashes them for idempotency.
3. **Dispatcher**: routes the payload to a transport handler based on `payload.type`.
4. **Transport handlers**: each owns one delivery method. The email handler delegates to TinkerWire's mailer; SMS will delegate to the chosen SMS module; etc.
5. **Receipt writer**: on success or terminal failure, writes a receipt JSON to `receipts/` in the repo and commits + pushes.
6. **Audit log**: appends every action to a local rotating log on the authoritative PC.

## Payload Schema (v1, email with attachments)
```json
{
  "version": 1,
  "type": "email",
  "to": ["frankydlp@gmail.com"],
  "cc": [],
  "bcc": [],
  "subject": "string",
  "body": "string (plain text)",
  "attachments": ["path relative to repo root or absolute path on host"],
  "from_alias": "optional, defaults to TinkerWire from_email",
  "request_id": "client-generated UUID for idempotency"
}
```

## Receipt Schema (v1)
```json
{
  "request_id": "matches payload",
  "status": "delivered | failed",
  "transport": "smtp",
  "delivered_at": "ISO 8601",
  "error": "string, present only on failed",
  "host": "TINKERSWORKSHOP"
}
```

## Known Constraints
- Daemon must run under an interactive user session to access Windows Credential Manager. SSH sessions and LocalSystem services cannot.
- The repo is private. Public-key SSH auth to GitHub is the supported access method.
- Attachments referenced by absolute path require the daemon to have read access on the host (so phone-originated payloads can only reference files already on the host or already committed in the repo).
- Single-tenant. One PC owns the keyring, one daemon delivers.
