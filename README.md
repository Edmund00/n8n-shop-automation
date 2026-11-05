# n8n Shop Automation

Small, practical automations for online shops, built with n8n. Each project lives in its own folder with a workflow file, a README and a test report that says honestly what was tested and what was not.

All examples use Stripe **test mode** and sample data only. No real keys, no real customer data.

## Projects

| Project | What it does | Status |
|---|---|---|
| [order-confirmation](order-confirmation/) | A paid Stripe test checkout creates a row in a Google Sheet and sends the customer a short confirmation email. Errors send an alert email. | Imported and partly tested locally (import OK, data normalization verified). Live Stripe, Google Sheets and SMTP not yet tested. |
| [product-texts-ai](product-texts-ai/) | Product list in a sheet becomes product descriptions and short social posts written by an AI model, released after manual approval. | Imported and partly tested locally (import OK, validation and selection logic run with sample data, one fix after review). Live Sheets, OpenAI and SMTP not yet tested. |
| [daily-report](daily-report/) | Every morning at 07:00 a short summary of yesterday's orders, revenue and top product by email. | Imported and partly tested locally (import OK, calculation run with sample data incl. zero orders and error cases). Live Sheets and SMTP not yet tested. |

## How the work is done

The workflows are drafted with AI assistance (Claude), then reviewed and tested by hand. Corrections made during review are listed in each test report.

Notes on running n8n locally for free: [docs/n8n-lokal-installieren.md](docs/n8n-lokal-installieren.md)

## Known limitations

- Local import and sample-data checks of the Code nodes passed. Live integrations (Stripe, Google Sheets, OpenAI, SMTP) and complete workflow runs are not tested yet.
- Overlapping runs may process a product twice, and product updates rely on stable sheet row positions.
- The daily report reads the whole sheet and assumes one row per order. Orders with several products would need a different model.

## License

MIT, see [LICENSE](LICENSE).
