# Calibration Reporting Standard (CRS): v0.1 Specification

[![Rights](https://img.shields.io/badge/rights-all_reserved-lightgrey.svg)](LICENSE)
[![SSRN](https://img.shields.io/badge/SSRN-7511058-red.svg)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7511058)
[![Schema](https://img.shields.io/badge/Schema-v0.1.0-green.svg)](crs-v0.1-schema.json)
[![Comments welcome](https://img.shields.io/badge/comments-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Status:** Draft for comment | **Version:** 0.1.0

**Notice:** Informational only; not legal, financial or regulatory advice. No reliance or warranty. This is a proposal by one author; no regulator has approved or endorsed it. Issues are public: do not post confidential or personal data.

A 13-field structured record format for reporting the calibration of autonomous AI agents in financial services. Draft specification.

---

## The Problem

When an autonomous AI agent makes a consequential financial decision, such as approving a loan, executing a trade or flagging fraud, there is currently no standard format for recording that the agent was calibrated, by whom, and under whose authorisation.

The public documents below do not define a calibration reporting format for autonomous AI agents:

- SR 26-2 (Fed/FDIC/OCC, April 2026) explicitly excluded agentic AI from its scope
- The FCA Mills Review (July 2026) recommended that the FCA consider leading the development of a trusted framework for AI agent participation in financial services (priority recommendation 5)
- MAS FEAT Principles (2018) set out fairness, ethics, accountability and transparency principles for AI in financial services but did not specify a standardised attestation format for agentic AI systems; FEAT predates agentic AI and later MAS material has not been assessed here
- The EU AI Act (Regulation (EU) 2024/1689) requires high-risk AI systems to technically allow automatic recording of events (Article 12(1)) but defines no calibration attestation format

CRS is a proposed answer to that question.

---

## What CRS Defines

A CRS attestation record is a structured document, compiled by the deploying institution and completed by an independent third-party attester, for a specific AI agent, covering a defined reporting period. It records 13 fields across three accountability dimensions:

### Attribution (Pillar 1)

| Field | Description |
|---|---|
| 1. `agent_did` | W3C DID uniquely identifying the AI agent |
| 2. `reporting_period_start` | Start of the calibration measurement period |
| 3. `reporting_period_end` | End of the calibration measurement period |
| 4. `system_scope` | Authorised decision categories, deployer DID, and authorisation chain reference |

### Disclosure (Pillar 2)

| Field | Threshold |
|---|---|
| 5. `calibration_rate` | Compliance: CR >= 0.80 (with ECE < 0.05); remediation required: CR < 0.80, or ECE from 0.05 to 0.10 inclusive (30-day window); see `docs/compliance-states.md` |
| 6. `false_positive_rate` | Recorded; no pass/fail threshold |
| 7. `expected_calibration_error` | Compliance: ECE < 0.05; remediation required: 0.05 <= ECE <= 0.10 (30-day); mandatory recalibration: ECE > 0.10 (72-hour) |
| 8. `human_review_rate` | Recorded; the author's proposed minimum is 0.001, a measure of human oversight not derived from any regulation; no supervisor has agreed to act on it |
| 9. `systematic_failure_disclosures` | Empty if no failures; populated with per-category CR/ECE values if failures occurred |
| 10. `reattestation_event_log` | Log of all material model updates triggering re-attestation |

### Governance (Pillar 3)

| Field | Description |
|---|---|
| 11. `attester_did` | W3C DID of the independent third-party attester |
| 12. `attestation_date` | Date the attestation was generated |
| 13. `regulatory_jurisdiction` | Jurisdiction(s) under which the attestation is issued |

Compliance determination (COMPLIANT / REQUIRES_REMEDIATION / MANDATORY_RECALIBRATION) is derived from fields 5 and 7 and not stored; it is computed at evaluation time. When several conditions hold, the most severe state applies (MANDATORY_RECALIBRATION > REQUIRES_REMEDIATION > COMPLIANT); see `docs/compliance-states.md`.

---

## Possible Uses

A CRS record is designed so that other parties could choose to reference it, for example insurers assessing AI agent liability or supervisors reviewing model risk. To the author's knowledge, no insurer or supervisor has adopted CRS. A CRS record is not evidence of insurability, regulatory compliance or capital treatment.

---

## Schema

The full JSON Schema (draft 2020-12) is in `crs-v0.1-schema.json`.

### Quick Reference

The schema is the file `crs-v0.1-schema.json` in this repository. All rights are reserved; you may read and evaluate it, and you should write to contact@vacra.ai before any other use.

---

## Contributing

Comments and feedback are welcome via GitHub Issues. See [CONTRIBUTING.md](CONTRIBUTING.md) for how to submit threshold reviews, review feedback, and schema issues. Pull requests are not accepted.

If you are working on AI agent governance, insurance underwriting for AI, or regulatory compliance tooling and see gaps or implementation challenges in this design, open an issue. The threshold values (CR 0.80, ECE 0.05/0.10) are the author's proposal and are open for review. The table below lists published work on the ECE metric for context; it does not set these thresholds:

| Paper | Domain | Finding | Relevance |
|---|---|---|---|
| Guo et al. (2017) ICML | Computer vision (foundational) | Reports ECE of about 0.2% to 2.4% after temperature scaling on the image datasets in its Table 1 | Context for the ECE metric: reports ECE below 5% after temperature scaling in image classification; not a derivation of the CRS threshold |

Full threshold analysis and supporting literature: see the reference paper (SSRN 7511058).

---

## Reference Paper

Chan, E.T.C. (2026). *Post-Consultation Position Paper: Attribution Infrastructure for Autonomous Financial Agents*. SSRN Working Paper 7511058. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7511058

## IP Notice

Two PCT international patent applications are pending (filed 2026). This specification is published as a draft for review; all rights are reserved and no licence is granted (see `LICENSE`). See `PATENTS.md` for the patent notice.

---

## Author

**E Chan**
ORCID: https://orcid.org/0009-0009-8249-7623
contact@vacra.ai
