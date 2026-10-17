# Text PDF to spreadsheet: a worked extraction example

Copying a PDF table into a spreadsheet is easier to check when every record points back to its source. This example shows a two-page text PDF, four extracted records, and the page, table and row references used to review them.

**All four products are invented.** This is SourceToSheet sample output, not a customer delivery, testimonial or sales result. No application or application source code is included.

## Inspect the source and output

1. Open [`sample-input.pdf`](sample-input.pdf). Each page contains one ruled table with two product records.
2. Open [`delivery/workbook.xlsx`](delivery/workbook.xlsx). **Prepared** contains the table; **Source Evidence** traces individual fields to their original location; **Page Coverage** accounts for both pages.
3. Compare the records below with [`delivery/prepared.csv`](delivery/prepared.csv) and the original PDF.
4. Read [`delivery/report.html`](delivery/report.html) locally for the review summary. The **Review Needed** sheet and [`delivery/review-needed.csv`](delivery/review-needed.csv) have no exceptions for this sample.

| SKU | Product | Price text | Source page | Source location |
| --- | --- | --- | --- | --- |
| `0007` | Linen shirt | `0012.50` | 1 | table 1, row 2 |
| `0008` | Canvas jacket | `29.00` | 1 | table 1, row 3 |
| `0009` | Cotton scarf | `8.00` | 2 | table 1, row 2 |
| `0010` | Wool cap | `15.00` | 2 | table 1, row 3 |

The result contains **4 records, 3 requested fields, 2 source-reference columns and 0 review exceptions**. The four records cover all 12 source field values. The header is row 1 of each source table, so the first product is row 2.

SKU and price values in the workbook are stored as text. When importing CSV, explicitly set these columns to text to retain leading zeroes and decimal places. No missing product facts or prices are invented during conversion.

## Rules and limits

[`delivery/rules.json`](delivery/rules.json) declares the three source columns and requires a non-negative decimal price. [`delivery/result.json`](delivery/result.json) includes the extracted records, field-level source locations and page coverage. Its **READY** status applies to this sample and these rules.

This example uses a simple ruled, text-based table. It does not demonstrate OCR, scans, handwriting or compatibility with every PDF layout. Source references help a reviewer check the result; they do not replace reading the original pages. No live store was updated.

## Files and provenance

The 11 original sample files are copied byte-for-byte from the [previously published sample ZIP](https://inu-gumi.pro/exportcheck/site/samples/source-to-sheet/source-to-sheet-sample.zip). Its SHA-256 is `7bc37afaaf9be5d97d091e5a75da60b32a94be4d7b703fe56fee3296d7e6f9aa`. This README adds the walkthrough. See [`START-HERE.txt`](START-HERE.txt) for the original notes and [`delivery/manifest.json`](delivery/manifest.json) for file hashes. You may inspect and reuse the invented sample data for evaluation.

## If you need this for your own file

Published by the maker of **[SourceToSheet](https://inu-gumi.pro/exportcheck/site/source-to-sheet)**, a file-conversion service starting at **$49** on Upwork. The initial scope is one non-personal, non-confidential text PDF, one consistent layout, up to 10 pages, 100 records, 8 requested fields and 20 MiB. Three-day delivery after complete requirements, one revision within the original scope, and permission for AI-assisted planning and review are required. Marketplace fees and taxes may apply.

Use the [Upwork offer](https://www.upwork.com/services/product/admin-customer-support-text-pdf-tables-converted-to-excel-with-source-page-references-2094924043265415041) to discuss uncertain layouts before ordering. Keep orders, messages, files and payments on Upwork. Do not post private documents or customer data in a public issue.

For another task, see the [CSV comparison](../README.md) or [supplier-column mapping](../mapping-example/README.md) examples.

For a general question about text PDFs, table layouts or source references, [ask a public workflow question](https://github.com/everlethe/exportcheck-csv-example/issues/new?template=workflow-question.md). Describe the layout without uploading your PDF. Existing Upwork orders stay in their Upwork conversation.
