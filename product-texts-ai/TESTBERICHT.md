# Test report: Product Texts with AI (05.11.2026)

Environment: n8n 2.46.6 locally on Windows (free Community version, command line only), Node 24.

## Passed
1. Import of `workflow.json` (8 nodes): "Successfully imported 1 workflow".
2. Code node "Select Pending Rows", run alone with sample rows: rows with an empty or missing status are selected (rows 2 and 4), a row with status `draft - needs approval` is skipped, a row with an invalid row number throws an error.
3. Code node "Validate Drafts", run alone: a valid answer becomes row_number + description_draft + post_draft + status `draft - needs approval`. Rejected as expected: text that is not JSON, text starting with `=` (formula), text over the word limit.
4. The language model node is connected to the AI node (`ai_languageModel` connection checked in the file).

## Correction made during review
- An AI answer wrapped in code fences (` ```json ... ``` `) was rejected. Fix: fences are stripped before parsing. Re-tested: now accepted.

## Not tested
- Real Google Sheets connection (read, update, `row_number` field in real results).
- Real OpenAI call and the quality of the generated texts.
- Whether the item pairing between "Select Pending Rows" and "Validate Drafts" holds with several rows in a live run.
- The alert email (SMTP) and the error outputs.
- The 15-minute schedule.

Method: the Code nodes were executed with a small Node script and sample data, not inside n8n. Only the import was done by n8n itself.
