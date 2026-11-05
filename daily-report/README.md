# Daily sales report

Every day at 07:00 the workflow reads the orders from a Google Sheet (`orderNumber`, `date`, `amountEur`, `productName`, `customerEmail`), keeps yesterday's orders (time zone Europe/Berlin), and emails a short summary: number of orders, revenue in EUR with two decimals, and the top product. With no orders the email says "No orders yesterday". Errors send an alert email.

Flow: Every Day at 07:00 -> Read Order Rows -> Calculate Yesterday Sales -> Send Daily Sales Summary. An error output sends an alert email.

## Rules in the calculation

- One row is one order. A duplicate order number stops the run with an error instead of counting twice.
- Dates: `YYYY-MM-DD` or an ISO timestamp with a time zone. Anything else is an error.
- Amounts must use a decimal point and at most two decimals (`12.50`, not `12,50`). Money is added in cents to avoid rounding errors.
- Test mode: put `__reportDate: '2026-11-04'` on the first input item to run the code node alone with a fixed day.

## Needed credentials (placeholders in the file)

- Google Sheets OAuth2 (read)
- SMTP for the summary and alert emails (use your own test account)

Replace every `REPLACE_WITH_...` value and the `example.com` addresses before use. The workflow is imported inactive. Use only synthetic orders or Stripe test-mode orders in the sheet.

## Status

Written by ChatGPT, reviewed and tested by hand. See [TESTBERICHT.md](TESTBERICHT.md).
