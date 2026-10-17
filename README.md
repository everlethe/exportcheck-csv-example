# Keyed CSV comparison: a worked acceptance-check example

Two CSV exports can look different because rows moved, numbers were rounded, or records actually changed. This small **synthetic dataset** shows how to distinguish those cases using an explicit record key and acceptance rules.

**Included:** before/after CSV files, a comparison profile, and the resulting HTML/JSON/CSV reports. All order and product values are invented. No customer data is included.

## Choose a worked example

| Your task | Example |
| --- | --- |
| Check whether two exports contain the same records and values | [Keyed CSV comparison](#try-the-example), below |
| Map supplier columns into a product template while preserving SKU and price text | [Supplier worksheet → product CSV](mapping-example/README.md): 3 invented products, 5 output columns and 7 recorded transformations |

Both examples include the input, explicit rules and expected output. You can inspect them without buying or installing an application.

## Try the example

1. Open [`fixtures/before.csv`](fixtures/before.csv) and [`fixtures/after.csv`](fixtures/after.csv).
2. Match records using **`order_id` + `line`**, not their row positions.
3. Compare `amount` with an absolute decimal tolerance of **0.01**. Compare the other fields exactly.
4. Allow **zero** added, removed or changed records.
5. Compare your result with the expected outcomes below. You can use any tool that implements these rules; this repository does not require installing ExportCheck.

## Expected result: FAIL

| Case | What changed | Expected treatment |
| --- | --- | --- |
| Row order | The same records appear in a different order | Match by the composite key; row position alone is not a change |
| Decimal tolerance | `SAMPLE-001` / `2`: `9.50` → `9.505` | Difference `0.005` is within `0.01`; accept |
| Changed field | `SAMPLE-002` / `1`: state `pending` → `paid` | One changed record |
| Added record | `SAMPLE-003` / `1` appears only in the second file | One added record |

**Counts:** 1 added, 0 removed, 1 changed, 2 unchanged; no empty or ambiguous keys. The zero-change acceptance rule therefore fails. This is the intended outcome, not a broken example.

- [Comparison profile](fixtures/profile.json)
- [Structured expected report](expected/report.json)
- [Expected differences](expected/differences.csv)
- [View the rendered report on the product site](https://inu-gumi.pro/exportcheck/site/demo/report.html)
- [Download the existing sample pack](https://inu-gumi.pro/exportcheck/site/sample-pack.zip)

The profile and report schema are from ExportCheck CLI 0.1.0. A different comparison tool may represent the same findings differently. These files demonstrate one small case and are not a benchmark or a guarantee for other data.

## Use it in your own workflow

Before accepting a migration or recurring export, write down the record key, fields that may vary, decimal tolerances, and permitted additions/removals. A green-looking spreadsheet is not an acceptance rule.

Keep identifiers as text, choose keys that uniquely identify a record, and inspect unexpected differences before accepting an export. The same checklist is useful even when you compare files manually.

## About ExportCheck

This repository is published by the maker of ExportCheck. It contains the free worked example, **not the commercial application or its source code**.

- **[ExportCheck CLI](https://inu-gumi.pro/exportcheck/site/)** — local CSV acceptance checks; $19 one-time single-user commercial licence, plus applicable tax. Python 3.11+; macOS and Ubuntu tested. [Requirements and commands](https://inu-gumi.pro/exportcheck/site/quickstart).
- **[ExportCheck Desk](https://inu-gumi.pro/exportcheck/site/exportcheck-desk)** — desktop CSV/Excel comparison; $39 one-time, plus applicable tax. See the product page for Mac/Windows requirements and current download details.

You may use these synthetic fixtures to evaluate a comparison workflow. For product questions, use the [support page](https://inu-gumi.pro/exportcheck/site/support). Never post private exports, credentials or customer data in a public issue.
