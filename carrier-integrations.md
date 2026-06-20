# Carrier Integrations

Carrier integrations connect Diversifi to your carrier accounts so that carrier invoices can be pulled in automatically for reconciliation. Instead of manually uploading invoice files, carrier integrations keep your invoice data current and let Diversifi match carrier charges against WMS order data automatically.

## How Carrier Invoice Ingest Works

When a carrier sends an invoice, Diversifi ingests it — either automatically via a carrier integration or manually via file upload — and runs it through the reconciliation engine. Each line item on the invoice is matched against the corresponding WMS order to verify the carrier charged what was expected:

- **Matched** — the carrier charge matches the expected rate. No action required.
- **Discrepancy** — the carrier charged more or less than expected. Flagged for review.
- **Unmatched** — a carrier invoice line has no corresponding WMS order. Could be a voided label, a data sync gap, or a carrier billing error.

## Trackstar

Trackstar is the integration layer that powers carrier account connections in Diversifi. When you connect a carrier account, Diversifi connects to it through Trackstar, which handles the secure authentication and data retrieval from the carrier's systems. Trackstar:

- Connects to your carrier account using your account credentials
- Retrieves carrier invoices automatically on a sync schedule
- Passes invoice data to Diversifi for reconciliation
- Encrypts all data in transit and at rest — your carrier credentials are never stored in plain text

## Supported Carriers for Invoice Ingest

| Carrier | Notes |
|---------|-------|
| **FedEx** | Automatic ingest via Trackstar. Full invoice support including surcharges, adjustments, and accessorial fees. |
| **UPS** | Automatic ingest via Trackstar. Full invoice support. |
| **USPS** | Automatic ingest via Trackstar. Full invoice support. |
| **DHL eCommerce Solutions** | Automatic ingest via Trackstar. |
| **BuKuShip / Reseller invoices** | Supported via file upload. BuKuShip is a parcel rate reseller — invoices follow a different format from standard carrier invoices and are handled separately. |

## Connecting a Carrier via Trackstar

1. Navigate to the carrier's billing settings page
2. Enter your carrier Account Username and Account Password
3. Check the box to allow Diversifi to retrieve billing information from this carrier
4. Click Connect Billing — the Trackstar connection modal will appear
5. Review the connection details and click Continue to authorize

{% hint style="info" %}
The Connect Billing button only enables when all three required fields are complete — Account Username, Account Password, and the billing permission checkbox. If the button is grayed out, check that all three are filled in.
{% endhint %}

**Connection status** — Once connected, the carrier integration shows a Connected status. If the connection fails or credentials expire, the status updates and you'll need to re-enter your credentials and reconnect.

## Manual Invoice Upload

If you prefer not to connect a carrier account via Trackstar, or if a carrier is not yet supported for automatic ingest, you can upload invoice files manually. Diversifi supports CSV and Excel invoice formats from all major carriers.

1. Navigate to Invoice Ingest in the Billing section
2. Click Upload Invoice and select your file
3. The Data Mapper processes the file and maps the invoice lines to Diversifi's internal format
4. Review the mapping and confirm — the invoice will then be available for reconciliation

## Invoice Deduplication

Diversifi automatically detects and skips duplicate invoices on ingest. If you upload the same invoice file twice, or a carrier sends the same invoice line through the integration more than once, Diversifi skips the duplicate and notifies you — it will not create duplicate records in your reconciliation data.

## Surcharge Data and Reconciliation Accuracy

Reconciliation accuracy depends on having complete surcharge data configured for each carrier rate set in Cost Rates. If surcharge data is missing — DAS, residential, AHS, fuel discount — the platform will flag a warning but still process the invoice. Missing surcharge data means the expected charge calculation may not match what the carrier actually billed, which produces more discrepancy flags than necessary.

To maximize reconciliation accuracy, ensure DAS, residential, AHS, and fuel discount values are configured for every active rate set. See [Carrier Configuration](../bidboost/carrier-configuration.md).
