# Security Policy

## Scope

This repository contains a specification document (CRS v0.1) and a JSON Schema.
There is no executable software in this repository.

Security concerns relevant to this project include:

- **Schema vulnerabilities**: a field definition or validation rule that could
  allow a malformed CRS record to pass validation and produce a false compliance
  signal in a regulated system
- **Example record issues**: sample data in  that could be
  misinterpreted as a real attestation record
- **Documentation errors**: specification language that could be misimplemented
  in a way that creates a compliance gap

## Reporting

To report a security or integrity concern, please email **chan629@purdue.edu**
with the subject line .

Do not open a public GitHub issue for security-sensitive findings.

**What to include:**
- Which file and field is affected
- The specific scenario in which the issue could be exploited or misinterpreted
- A suggested remediation if you have one

## Response

Reports will be acknowledged within 5 business days. Valid findings will result
in a schema patch release and a note in the release changelog crediting the
reporter (unless anonymity is requested).

## Out of scope

- Social engineering attacks
- Issues in third-party tools that consume CRS records (report to those maintainers)
- Threshold value disagreements (use the threshold-review issue template instead)
