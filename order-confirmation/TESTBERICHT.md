# Testbericht Order Confirmation (05.11.2026)

Umgebung: n8n 2.46.6 lokal auf Windows (kostenlose Community-Version, nur Kommandozeile, kein Server, keine Anmeldung), Node 24.

## Bestanden
1. Import des Original-Workflows (workflow.json, 5 Knoten): "Successfully imported 1 workflow". n8n akzeptiert die Datei.
2. Ausfuehrung der Test-Variante (Manual Trigger, Beispiel-Stripe-Ereignis, dann "Normalize Order Data"): Status success.
   Eingabe: checkout.session.completed mit id cs_test_a1B2c3D4, amount_total 3990, created 1793900000, E-Mail kunde@example.com, metadata.product_name "Beispiel-Produkt".
   Ausgabe: orderNumber cs_test_a1B2c3D4, date 2026-11-05, amountEur 39.90, productName Beispiel-Produkt, customerEmail kunde@example.com.

## Nicht getestet
- Echte Stripe-Verbindung (Webhook, Testzahlung), weil der Laptop keine oeffentliche Adresse hat.
- Google-Sheets-Anhaengen und E-Mail-Versand (SMTP): dafuer fehlen Zugangsdaten; nur der Aufbau wurde von n8n akzeptiert.
- Fehlerzweig (Fehler-Mail).
- Randfaelle (leeres Ereignis liefert laut Code "unknown", 0.00, "Online order", leere E-Mail; nicht ausgefuehrt).

## Hinweis zur Installation
Mit npx n8n scheiterte die Installation (ein Hilfspaket verlangt playwright-core 1.65.0, in der Paketquelle nicht vorhanden). Loesung: package.json mit overrides auf 1.64.1 (siehe docs/n8n-lokal-installieren.md). npm 11 hat einige Installationsskripte uebersprungen; fuer Import und Ausfuehrung war das kein Problem.
Test-Dateien: test/test-normalize.json, test/original-mit-id.json (in diesem Ordner).
