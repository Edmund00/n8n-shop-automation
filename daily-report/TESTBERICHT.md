# Test report: Daily Sales Report (05.11.2026)

Environment: n8n 2.46.6 locally on Windows (free Community version, command line only), Node 24.

## Passed
1. Import of `workflow.json` (5 nodes): "Successfully imported 1 workflow".
2. Code node "Calculate Yesterday Sales", run alone with sample data and the fixed date 2026-11-04:
   - Normal day: 3 orders (39.90 + 19.10 + 39.90), result "Orders: 3, Revenue: EUR 98.90, Top product: Alpha (2 orders)". An order from another day and an empty row were ignored. An ISO timestamp with `Z` was accepted.
   - No orders for that day: "No orders yesterday, Orders: 0, Revenue: EUR 0.00".
   - Duplicate order number: error as designed.
   - Amount `12,50` (comma): error as designed.

## Not tested
- Real Google Sheets connection and the real column format (for example whether dates come as text or as numbers).
- The summary email and the alert email (SMTP), the error output.
- The 07:00 schedule and the "yesterday" calculation on a real day (only the fixed test date was used).
- Orders around midnight in other time zones, orders with several products per order (not supported: one row per order).

Method: the Code node was executed with a small Node script and sample data, not inside n8n. Only the import was done by n8n itself.
