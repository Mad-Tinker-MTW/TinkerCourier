# Schedule
**TinkerCourier**
Document ID: TCRR-PMD-005
Version: 1.0
Date: 2026-06-14
Project Manager: Francisco De La Paz

---

## Schedule Approach

TinkerCourier is built in four stages. Each stage is a usable increment: Stage 1 ships a working email dispatcher; Stage 2 makes it production-grade on a single host; Stage 3 extends the transport set; Stage 4 wires it into the rest of the MTW ecosystem. Hour estimates use single-project focused effort with one operator covering all roles, logged by role per the MTW labor standard.

---

## Stage-Level Schedule

| Stage | Description | Estimated Effort | Target |
|---|---|---|---|
| 1 | Minimum Courier (email via TinkerWire) | 28 hrs | TBD |
| 2 | Hardening and Scheduled Task | 16 hrs | TBD |
| 3 | Reach (SMS, Discord, Slack) | 24 hrs | TBD |
| 4 | Ecosystem Integration | 20 hrs | TBD |
| | **Total** | **88 hrs** | |

---

## Stage 1 Effort Breakdown by Role

| Role | Hours |
|---|---|
| Project Manager | 2 |
| Solutions Architect | 4 |
| Lead Developer | 16 |
| Technical Writer | 2 |
| QA Engineer | 2 |
| Deployment Engineer | 2 |
| **Stage 1 Total** | **28** |

---

## Stage 2 Effort Breakdown by Role

| Role | Hours |
|---|---|
| Project Manager | 1 |
| Solutions Architect | 2 |
| Lead Developer | 8 |
| Technical Writer | 1 |
| QA Engineer | 2 |
| Deployment Engineer | 2 |
| **Stage 2 Total** | **16** |

---

## Stage 3 Effort Breakdown by Role

| Role | Hours |
|---|---|
| Project Manager | 2 |
| Solutions Architect | 3 |
| Lead Developer | 14 |
| Technical Writer | 1 |
| QA Engineer | 2 |
| Deployment Engineer | 2 |
| **Stage 3 Total** | **24** |

---

## Stage 4 Effort Breakdown by Role

| Role | Hours |
|---|---|
| Project Manager | 2 |
| Solutions Architect | 3 |
| Lead Developer | 12 |
| Technical Writer | 1 |
| QA Engineer | 1 |
| Deployment Engineer | 1 |
| **Stage 4 Total** | **20** |

---

## Dependencies

- TinkerWire mailer must remain stable (it owns SMTP credentials and the actual send).
- GitHub SSH-key auth must be configured on both the host and any client device that pushes payloads.
- Stage 4 integrations depend on the consuming projects (MessageBurst, HexVeridicae) being at a point where they want Courier as their dispatch back-end.

---

## Notes

Stage 1 is intentionally generous because the payload schema and the receipt model set the contract for every later stage. Investing the right amount of design time here pays off across all four stages.
