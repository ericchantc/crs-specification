# CRS Compliance States

Compliance state is computed from the attestation record at evaluation time. It is not stored in the record itself.

## Determination logic

```
if CR >= 0.80 AND ECE < 0.05:
    state = COMPLIANT

elif CR < 0.80 OR (ECE >= 0.05 AND ECE <= 0.10):
    state = REQUIRES_REMEDIATION

elif ECE > 0.10:
    state = MANDATORY_RECALIBRATION
```

## States

### COMPLIANT

All primary thresholds met. A verifiable credential may be issued. The deploying institution may represent the agent as CRS-compliant for the attested reporting period.

Condition: `calibration_rate >= 0.80 AND expected_calibration_error < 0.05`

### REQUIRES_REMEDIATION

One or more thresholds missed. Re-attestation required within **30 calendar days**. The agent may continue operating, but the deploying institution must initiate a recalibration or model review process.

Condition: `calibration_rate < 0.80` OR `(expected_calibration_error >= 0.05 AND expected_calibration_error <= 0.10)`

### MANDATORY_RECALIBRATION

Calibration error exceeds the emergency threshold. Re-attestation required within **72 hours**. The attestation credential is withheld pending successful re-attestation. Continued operation without re-attestation constitutes a breach of the CRS reporting obligation.

Condition: `expected_calibration_error > 0.10`

## Notes on human_review_rate

A `human_review_rate` below 0.001 (fewer than 1 in 1,000 autonomous decisions reviewed by a qualified human) does not trigger a MANDATORY_RECALIBRATION state on its own. It triggers a supervisory adequacy review — a separate governance obligation under applicable AI accountability frameworks (EU AI Act Art. 9, MAS FEAT).

## Notes on systematic_failure_disclosures

A non-empty `systematic_failure_disclosures` array does not by itself change the compliance state. It is a mandatory transparency field. Failure to report known systematic failures when they exist is the compliance violation — not the failures themselves.
