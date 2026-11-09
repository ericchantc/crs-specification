# Integration Guide

This guide describes an unfinished draft. Nothing in it gives permission to implement or pilot CRS, and the example record below is illustrative: its values are invented.

A CRS attestation record is a JSON document conforming to [`crs-v0.1-schema.json`](../crs-v0.1-schema.json). The deploying institution compiles fields F1 to F10 after a calibration measurement period, and an independent third-party attester completes F11 to F13. CRS v0.1 defines no signing mechanism. How records are distributed is outside the scope of CRS v0.1.

## Attestation lifecycle

```
1. MEASURE     Deploying institution collects prediction/outcome pairs
               over the reporting period (a 90-calendar-day period is preferred).
               Computes CR (F5), FPR (F6), ECE (F7), human_review_rate (F8).

2. ATTEST      An independent third party reviews the measurements
               and completes F11 to F13 (attester DID, attestation date,
               jurisdictions).

3. DELIVER     The completed record is provided to the party that asked for it.
               Whoever relies on a record computes the compliance state
               from F5 and F7 (docs/compliance-states.md).

4. RE-ATTEST   A re-attestation trigger starts a new cycle. The windows in
               docs/compliance-states.md are the author's proposal.
```

## Example attestation record

```json
{
  "agent_did": "did:web:agents.bank.example.com:trade-execution-v3",
  "reporting_period_start": "2026-07-01",
  "reporting_period_end": "2026-09-28",
  "system_scope": {
    "decision_categories": ["equity_trade_execution", "portfolio_rebalancing"],
    "deployer_did": "did:web:bank.example.com",
    "authorization_chain_reference": "sha256:c2f02b0e098f344593ccf86647c4ce727d5f927df1de0ae24224846fe66ab90f"
  },
  "calibration_rate": 0.87,
  "false_positive_rate": 0.04,
  "expected_calibration_error": 0.032,
  "human_review_rate": 0.005,
  "systematic_failure_disclosures": [],
  "reattestation_event_log": [],
  "attester_did": "did:web:auditor.example.org",
  "attestation_date": "2026-09-30",
  "regulatory_jurisdiction": ["MAS", "HKMA"]
}
```

Compliance state for this record: **COMPLIANT** (CR = 0.87 >= 0.80; ECE = 0.032 < 0.05).

## DID infrastructure

Both `agent_did` (F1) and `deployer_did` (in F4) use W3C Decentralized Identifiers (DIDs). The schema checks the DID format only; it does not resolve DIDs.

DID specification: https://www.w3.org/TR/did-core/
