# Supplier worksheet to product CSV: a worked mapping example

A supplier worksheet has `Supplier SKU`, `Item`, `Options` and `Unit Price`. Your import template needs `SKU`, `Product`, `Color`, `Size` and `Price`. This example shows the exact mapping, the expected output, and a change log you can inspect before importing anything.

**All three products are invented.** This is a sample of CatalogOps Import Prep output, not a customer delivery, testimonial or sales result. It includes no application or application source code.

## Inspect the input and rules

1. Open [`sample-input.xlsx`](sample-input.xlsx), sheet **Products**.
2. Read [`delivery/rules.json`](delivery/rules.json) and [`delivery/mapping.csv`](delivery/mapping.csv).
3. Compare the expected CSV below with [`delivery/prepared.csv`](delivery/prepared.csv).
4. Inspect [`delivery/changes.csv`](delivery/changes.csv) for each transformation. No source row is removed or merged, and no missing product fact is invented.

| Source column | Output column | Rule |
| --- | --- | --- |
| Supplier SKU | SKU | Exact copy; keep leading zeroes |
| Item | Product | Trim outer whitespace |
| Options | Color | Split on the literal `\|`, take the first of exactly two parts, trim outer whitespace |
| Options | Size | Split on the literal `\|`, take the second of exactly two parts, trim outer whitespace |
| Unit Price | Price | Exact copy; validate as a non-negative decimal without changing its text |

For example, the first row has SKU `0007`, Item `  Linen shirt  `, Options `Blue | M` and Unit Price `0012.50`. The name loses its outer spaces, the options become two fields, and the SKU and price text stay unchanged.

## Expected output

```csv
SKU,Product,Color,Size,Price
0007,Linen shirt,Blue,M,0012.50
0008,Canvas jacket,Olive,L,29.00
0009,Cotton scarf,Sand,One size,8.00
```

The output contains **3 records, 5 columns, 7 recorded transformations and 0 review exceptions**. The seven transformations are one product-name trim and six split outputs. This count describes transformed values, not seven changed products.

[`delivery/workbook.xlsx`](delivery/workbook.xlsx) includes **Prepared**, **Original**, **Changes**, **Mapping** and **Review Needed** sheets. It stores values as text to preserve identifiers and price formatting. When importing the CSV into a spreadsheet, explicitly choose text columns for SKU and Price; opening it directly may reinterpret those values.

The sample status is **READY for these declared rules**. It does not demonstrate acceptance by a particular store or marketplace. Check your destination's required fields and rules before importing. No live store was updated.

## Files and provenance

- [`delivery/report.html`](delivery/report.html): download and open locally for the readable summary.
- [`delivery/result.json`](delivery/result.json): structured result.
- [`delivery/review-needed.csv`](delivery/review-needed.csv): header only, because this sample has no exceptions.
- [`delivery/manifest.json`](delivery/manifest.json): hashes of the input and delivery files.
- [`START-HERE.txt`](START-HERE.txt): original sample notes and service scope.

These 12 sample files were copied byte-for-byte from the [previously published sample ZIP](https://inu-gumi.pro/exportcheck/site/samples/import-prep/import-prep-sample.zip). The ZIP's SHA-256 is `1959e252c4c61c7122b2072401b8140e6cba9ce63b3c47df5fe71ed0ec8f7200`. This README is an additional walkthrough. You may inspect and reuse the invented sample data for evaluation.

## If you need this for your own file

Published by the maker of CatalogOps Import Prep and CatalogBridge:

- **[CatalogOps Import Prep](https://inu-gumi.pro/exportcheck/site/import-prep)** is a file-preparation service, starting at **$59** on Upwork. The initial scope is one non-personal, non-confidential UTF-8 CSV or XLSX worksheet, up to 100 rows, 20 source/output columns and 20 MiB, using your target template and up to three explicit trim/split rules. Three-day delivery after complete requirements, one revision within the original scope, and permission for AI-assisted processing are required. Marketplace fees and taxes may apply. Keep orders, messages, files and payments on Upwork.
- **[CatalogBridge](https://inu-gumi.pro/exportcheck/site/catalogbridge)** is separate desktop software for mapping CSV/Excel columns yourself, **$49 one-time**, plus applicable tax. See its page for supported platforms, limits and download details. This sample was produced by the Import Prep service tool; it is not a demonstration of the CatalogBridge interface.

For a before/after acceptance check rather than column mapping, see the [keyed CSV comparison example](../README.md). Use the [support page](https://inu-gumi.pro/exportcheck/site/support) for product questions. Do not post customer data, private files or credentials in a public repository.

Unsure whether you need a mapping service or a desktop tool? [Ask a public workflow question](https://github.com/everlethe/exportcheck-csv-example/issues/new?template=workflow-question.md) using only a general description or invented example. Existing Upwork orders stay in their Upwork conversation.
