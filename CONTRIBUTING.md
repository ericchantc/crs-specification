# Contributing to CRS

CRS is an open specification draft. Contributions take the form of expert feedback, threshold review, and implementation experience.

## How to contribute

### Open an issue

Use the issue templates to:
- **Threshold review** — challenge or support the CR >= 0.80 / ECE < 0.05 thresholds with empirical evidence
- **Implementation feedback** — share what you found when implementing CRS in a real system (gaps, ambiguities, edge cases)
- **Schema feedback** — missing fields, unclear definitions, or JSON Schema issues in `crs-v0.1-schema.json`

### Before you submit

- Check existing issues first
- Reference the relevant field name or pillar (e.g. F5 `calibration_rate`, Pillar 2)
- If citing a paper, include the DOI or arXiv ID

### What thresholds are open for challenge

All threshold values (CR >= 0.80, ECE < 0.05 / 0.10) are grounded in empirical calibration benchmarks and are explicitly open for challenge. If you have evidence from a specific deployment domain (medical AI, credit scoring, fraud detection), open a threshold-review issue — that is exactly the kind of feedback that improves the standard.

## IP notice

CRS is published under the Apache 2.0 license for open adoption. Two PCT international patent applications are pending (CRS-PCT-2026-001 and CRS-EXT-PCT-2026-001). See [PATENTS.md](PATENTS.md) for licensing details. Contributions to the specification itself do not transfer IP rights to contributors.

## Contact

For questions not suited to a public issue: chan629@purdue.edu
