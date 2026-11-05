# n8n Shop Automation

Small, practical automations for online shops, built with n8n. Each project lives in its own folder with a workflow file, a README and a test report that says honestly what was tested and what was not.

All examples use Stripe **test mode** and sample data only. No real keys, no real customer data.

## Projects

| Project | What it does | Status |
|---|---|---|
| [order-confirmation](order-confirmation/) | A paid Stripe test checkout creates a row in a Google Sheet and sends the customer a short confirmation email. Errors send an alert email. | Imported and partly tested locally (import OK, data normalization verified). Live Stripe, Google Sheets and SMTP not yet tested. |
| [product-texts-ai](product-texts-ai/) | Product list in a sheet becomes product descriptions and short social posts written by an AI model, released after manual approval. | Planned |
| [daily-report](daily-report/) | Every morning a short summary of sales and numbers by email. | Planned |

## How the work is done

The workflows are drafted with AI assistance (Claude), then reviewed and tested by hand. Corrections made during review are listed in each test report.

Notes on running n8n locally for free: [docs/n8n-lokal-installieren.md](docs/n8n-lokal-installieren.md)

## License

MIT, see [LICENSE](LICENSE).
