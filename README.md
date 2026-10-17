# Worked examples: CSV comparison, column mapping and PDF tables

Two CSV exports can look different because rows moved, numbers were rounded, or records actually changed. This small **synthetic dataset** shows how to distinguish those cases using an explicit record key and acceptance rules.

**Included:** before/after CSV files and comparison reports, a supplier worksheet with mapped output, and a text PDF with an extracted table and source references. All order and product values are invented. No customer data is included.

## Choose a worked example

- **Compare two CSV exports.** Follow the free [keyed CSV comparison](#try-the-example) below to distinguish moved rows, accepted rounding and actual changes. For your own files, run the checks with [ExportCheck CLI — $19](https://inu-gumi.pro/exportcheck/site/) or [ExportCheck Desk — $39](https://inu-gumi.pro/exportcheck/site/exportcheck-desk).

- **Map supplier columns into a product template.** The free [supplier worksheet → product CSV example](mapping-example/README.md) preserves SKU and price text across 3 invented products, 5 output columns and 7 recorded transformations. Order [CatalogOps Import Prep — $59 / 3 days](https://www.upwork.com/services/product/admin-customer-support-product-data-mapped-to-your-import-template-with-a-change-log-2094923219914975740), or map files yourself with [CatalogBridge — $49](https://inu-gumi.pro/exportcheck/site/catalogbridge).

- **Extract a text-PDF table with source references.** The free [text PDF → spreadsheet example](pdf-table-example/README.md) contains 2 pages, 4 invented products and page/table/row references. Order [SourceToSheet — $49 / 3 days](https://www.upwork.com/services/product/admin-customer-support-text-pdf-tables-converted-to-excel-with-source-page-references-2094924043265415041).

Each example includes the input, explicit rules and expected output. You can inspect them without buying or installing an application.

Prices are base USD; applicable tax and Upwork fees may be added. Software prices are one-time per user. The services cover small, single-file tasks: check the linked offer's input limits before ordering. Service delivery starts after complete requirements, includes one revision within the agreed scope, and requires sharing rights, explicit permission for OpenAI/ChatGPT processing, and non-personal, non-confidential data. Keep service orders, messages, files and payments on Upwork; do not upload your file to this public repository.

## Ask whether your workflow fits

[Ask a public workflow question](https://github.com/everlethe/exportcheck-csv-example/issues/new?template=workflow-question.md) if you are unsure which example or product fits. Describe the file type, approximate size and result you need; use invented values for any example. Questions may be answered by the owner's AI assistant.

Issues are public. Do not attach real files, customer information, credentials or payment references. For an existing Upwork order, continue in its Upwork conversation. Use [private product support](https://inu-gumi.pro/exportcheck/site/support) for account, purchase or delivery questions. A public discussion is not an order or a promise to accept work.

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
