# Product texts with AI

A Google Sheet lists products (`name`, `features`, `price`, `status`). Every 15 minutes the workflow picks up rows with an empty `status`, asks an AI model for a short product description (max 80 words) and a short social media post (max 40 words), and writes both back into the sheet as drafts with the status `draft - needs approval`. Nothing is published automatically. A human reads and approves the drafts.

Flow: Every 15 Minutes -> Read Product Rows -> Select Pending Rows -> Generate Product Drafts (OpenAI Chat Model) -> Validate Drafts -> Save Drafts for Approval. Every step has an error output that sends an alert email.

## Safety checks in the workflow

- Product fields are treated as untrusted data in the prompt (no instructions from the sheet).
- The AI must use only the supplied facts (no invented benefits, discounts or claims).
- The answer is validated: valid JSON, both fields present, word limits respected, no text starting with `=`, `+`, `@` or `-` (spreadsheet formula injection). Optional code fences around the JSON are removed.

## Needed credentials (placeholders in the file)

- Google Sheets OAuth2 (read and update)
- OpenAI API and a model name (`REPLACE_WITH_OPENAI_MODEL_NAME`)
- SMTP for the alert email (use your own test account)

Replace every `REPLACE_WITH_...` value and the `example.com` addresses before use. The workflow is imported inactive.

## Status

Written by ChatGPT, reviewed and tested by hand. See [TESTBERICHT.md](TESTBERICHT.md) for what was tested and what was not.
