# CRS Compliance States

Compliance state is computed from the attestation record at evaluation time. It is not stored in the record itself.

## Determination logic

```
if ECE > 0.10:
    state = MANDATORY_RECALIBRATION      # whatever CR is
elif CR < 0.80 OR (ECE >= 0.05 AND ECE <= 0.10):
    state = REQUIRES_REMEDIATION
else:
    state = COMPLIANT                    # CR >= 0.80 AND ECE < 0.05
```

**Precedence.** States are ordered MANDATORY_RECALIBRATION > REQUIRES_REMEDIATION > COMPLIANT, and the determination is the most severe state whose condition holds. The three conditions below overlap when `calibration_rate < 0.80` and `expected_calibration_error > 0.10`; such a record is MANDATORY_RECALIBRATION. Worked cases: CR 0.60 / ECE 0.20 is MANDATORY_RECALIBRATION; CR 0.795 and CR 0.80 at ECE 0.1025 are both MANDATORY_RECALIBRATION (a lower CR never gives a milder state).

> Proposed by the author. This draft creates no legal or regulatory obligation.

## States

### COMPLIANT

All primary thresholds met. The record reports a COMPLIANT state for the attested reporting period. This is not an assessment of safety, security or suitability for any use.

Condition: `calibration_rate >= 0.80 AND expected_calibration_error < 0.05`

### REQUIRES_REMEDIATION

One or more thresholds missed. Under the author's proposal, re-attestation is expected within **30 calendar days**. The deploying institution is expected to initiate a recalibration or model review process.

Condition: `calibration_rate < 0.80` OR `(expected_calibration_error >= 0.05 AND expected_calibration_error <= 0.10)`, applying only when `expected_calibration_error <= 0.10` (see Precedence)

### MANDATORY_RECALIBRATION

Calibration error exceeds the emergency threshold. Under the author's proposal, re-attestation is expected within **72 hours**. The 30-day and 72-hour windows are the author's proposal; they are not obligations imposed by any authority.

Condition: `expected_calibration_error > 0.10`

## Notes on human_review_rate

A `human_review_rate` below 0.001 (fewer than 1 in 1,000 autonomous decisions reviewed by a qualified human) does not change the compliance state. It is a disclosure field. The 0.001 value is the author's proposal; it is not an obligation stated in the EU AI Act or MAS FEAT.

## Notes on systematic_failure_disclosures

A non-empty `systematic_failure_disclosures` array does not by itself change the compliance state. It is a disclosure field. The `failure_type` values describe CR below the floor, ECE above the emergency level, or both; an ECE in the remediation band has no value in v0.1.
