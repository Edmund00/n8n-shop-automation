# Order Confirmation (n8n, Stripe test mode)

Small e-commerce automation: a paid Stripe test checkout creates a row in a Google Sheet and sends the customer a short confirmation email. Any failure sends an alert email.

**Test mode only.** No live keys, no real customer data. Status: imported and partly tested locally with n8n 2.46.6 (import OK, data normalization verified with a sample Stripe event). Not yet tested: live Stripe webhook, Google Sheets, SMTP. See TESTBERICHT.md.

## What it does
1. Stripe Trigger: event `checkout.session.completed`.
2. Code node: normalizes order number, date, amount (EUR), product name, customer email.
3. Google Sheets: appends a row to the tab "Bestellungen".
4. Email (SMTP): sends the customer a short confirmation (German text).
5. On any error: sends an alert email ("Fehler im Workflow").

The confirmation says the invoice follows later. Creating the invoice itself is a possible next step (PDF or Stripe invoice).

## Required n8n credentials
- `Stripe Test` (Stripe API, test secret key)
- `Google Sheets` (Google Sheets OAuth2)
- `SMTP` (SMTP account)

## Setup
1. n8n: Workflows > Import from File > `workflow.json`.
2. Create the three credentials and assign them to the nodes.
3. Create a Google Sheet with tab "Bestellungen" and header row: Bestellnummer, Datum, Betrag EUR, Produkt, Kunden-E-Mail. Put the sheet ID into the Sheet node.
4. Replace `shop@example.com` and `admin@example.com` in both email nodes.
5. Activate the workflow. The Stripe Trigger node registers its webhook in your Stripe test account automatically.

## Test
Create a Checkout Session in Stripe test mode and pay with card `4242 4242 4242 4242` (any future expiry, any CVC). Check the new sheet row and the confirmation email. Optional: set `metadata.product_name` on the session to fill the product column.
