# Data Asset Licensing Policy — Re-certification Rules (rev. 2026.10)

## Scope

Every asset recorded in `catalog/assets.csv` must be certified once per quarter.
The re-certification reference date for this cycle is **2026-11-09** (the date the
review is executed).

## Status and remediation rules

Evaluate the rules in the order listed below. The **first rule that matches**
determines both the certification status and the remediation code; once a rule
matches, do not apply any later rule.

| # | Condition | Status | Remediation code |
|---|-----------|--------|------------------|
| 1 | `contract_expiry` is earlier than the reference date | `EXPIRED` | `RENEW` |
| 2 | `contains_pii` is TRUE and `license_tier` is C or D | `BLOCKED` | `DECOMMISSION` |
| 3 | `redistribution` is `prohibited` | `BLOCKED` | `DECOMMISSION` |
| 4 | `license_tier` is C | `CLEARED_RESTRICTED` | `ANNOTATE` |
| 5 | `license_tier` is A or B and `redistribution` is `permitted` or `restricted` | `CLEARED` | `NONE` |
| 6 | any other combination | `MANUAL_REVIEW` | `ESCALATE` |

## Quarterly attestation

- The cycle is **NOT_ATTESTED** if at least one asset resolves to `BLOCKED` or
  `EXPIRED`. In that case the quarterly attestation ticket stays **open** and
  must receive a comment that names every affected asset ID.
- Otherwise the cycle is **ATTESTED**: comment on the quarterly attestation
  ticket and **close** it.

## Remediation tickets

Open one ticket per asset whose remediation code is `DECOMMISSION` or `RENEW`,
titled `Remediation required: <asset_id>`.

## Certification table

Commit the result to `compliance/recertification_q4_2026.csv`. The table has exactly three columns —
`asset_id`, `status`, `remediation_code` — one row per asset, in inventory
order, with no extra rows or columns.
