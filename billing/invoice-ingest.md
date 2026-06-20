# Invoice Ingest

Invoice ingest is how carrier invoices get into Diversifi. Once invoices are in the platform, Diversifi matches them against your WMS shipment data, applies your billing rules, and uses them as the basis for generating customer bills. Getting invoice ingest set up correctly is one of the most important steps in getting billing working accurately.

## How Invoice Ingest Works

When a carrier completes a delivery, they generate an invoice showing the actual cost of that shipment. That invoice needs to make it into Diversifi so the platform can:

- Compare the actual carrier cost against the quoted amount from your WMS
- Apply your markup rules to calculate what you bill your customer
- Capture any adjustments where the actual cost differs from the quote
- Ensure you are not paying for shipments you have already billed

Diversifi supports three ways to get invoices in — carrier integration via Trackstar, email ingest, and manual upload.

## Supported Carriers

Diversifi currently supports invoice ingest for the following carriers:

- FedEx
- UPS
- USPS
- DHL
- Amazon Shipping
- UniShippers UPS
- Vox / eHub
- Trackstar-connected carriers

**Multi-carrier reseller invoices** — Diversifi also supports ingestion of multi-carrier reseller invoice files. Resellers such as BuKuShip and eHub include multiple carriers and services on a single invoice file rather than one carrier per file. Diversifi identifies the source as the reseller name and maps each line item to the correct carrier and service from the data within the file. Per-customer mapping configuration is available if reseller file structures vary between customers.

## Carrier Integration via Trackstar

The recommended way to get invoices into Diversifi is through a carrier integration. Diversifi uses Trackstar to connect to carrier accounts and pull invoices automatically on a recurring basis.

**To connect a carrier account** — Go to Billing → Carrier Cost → Integrations and select the carrier you want to connect. Enter your carrier account credentials and Diversifi will begin pulling invoices automatically.

**What gets pulled** — Diversifi pulls all available invoices from the carrier account. Each invoice line item is mapped to a tracking number, carrier, service, and charge type. The data flows directly into your invoice ingest queue without any manual action required.

{% hint style="warning" %}
Do not use both carrier integration and email ingest for the same carrier at the same time. Running both will result in duplicate invoices being loaded. Use one method per carrier — carrier integration is preferred where available.
{% endhint %}

## Email Ingest

Email ingest lets you receive carrier invoices by forwarding invoice emails directly to a Diversifi inbox. This is useful for carriers not yet supported via direct integration, or for reseller invoices that arrive as email attachments.

**To set up email ingest** — Go to Billing → Carrier Cost → Invoice Ingest and find your account's dedicated ingest email address. Forward carrier invoice emails to this address and Diversifi will process the attachments automatically.

**Supported file formats** — Excel (.xlsx), CSV, and JSON invoice files are supported via email ingest.

**Processing time** — Invoices sent via email ingest are typically processed within a few minutes of receipt. They appear in your invoice ingest queue once processing is complete.

## Manual Upload

If you need to upload an invoice file directly without email, you can do so from the invoice ingest page.

**To manually upload an invoice** — Go to Billing → Carrier Cost → Invoice Ingest and click Upload Invoice. Select the file from your computer and choose the carrier it belongs to. Diversifi will process the file and add the line items to your ingest queue. Manual upload is useful for one-off situations or when setting up a new carrier before email ingest or integration is configured.

## Duplicate Detection

Diversifi automatically detects and prevents duplicate invoices from being loaded. If the same invoice is submitted twice — whether through email ingest, carrier integration, or manual upload — Diversifi identifies it as a duplicate and skips it rather than processing it again.

**How it works** — Diversifi checks each incoming invoice against existing records at the line item level, comparing tracking number, charge amount, charge type, and date. If a line item matches an existing record exactly, it is flagged as a duplicate and skipped. A notification is surfaced so you can see what was skipped and why.

**If a duplicate is loaded accidentally** — Go to Billing → Carrier Cost → Invoice Ingest, find the duplicate ingest record, and delete it. You can only delete an ingest if the invoices within it have not already been linked to bills. If they have been linked, the adjustment workflow handles any corrections.

## Viewing and Managing Invoices

Go to Billing → Carrier Cost → Invoices to see all invoices that have been ingested into Diversifi.

- **Filtering invoices** — Use the carrier filter at the top of the page to filter by carrier. You can also filter by date range, status, and source.
- **Invoice source** — Each invoice shows where it came from: carrier integration, email ingest, or manual upload.
- **Failed invoices** — If an invoice fails to process, Diversifi logs the failure with a reason. Filter by status to see any failed ingests. Common causes include unsupported file formats, missing carrier mapping, or malformed invoice data.

## Important Notes on Extensiv

If you use Extensiv as your WMS, Extensiv does not consistently provide a quoted cost through its standard API. Most Extensiv users bill based on carrier invoice actuals rather than quoted amounts from the WMS. For Extensiv accounts we recommend configuring your billing cycle to use **carrier invoice by invoice date** rather than WMS shipments, which avoids the reconciliation complexity that comes from Extensiv's inconsistent quoted cost data.

If you need full quoted cost reconciliation through Extensiv, you will need to enable Extensiv's billing module and provide the separate API credentials for the billing API. Contact your Diversifi account manager to discuss this setup.

## Common Questions

**Can I use both carrier integration and email ingest for the same carrier?** No — using both for the same carrier will result in duplicate invoices. Use one method per carrier. Carrier integration via Trackstar is preferred where available.

**What happens if an invoice arrives after a billing period has closed?** It is captured as an adjustment in the next billing period. The Adjustments section of the bill shows the delta between what was originally billed and the actual carrier cost from the late invoice.

**Why is my invoice not showing up after I emailed it?** Check that the file was attached in a supported format (Excel .xlsx, CSV, or JSON). Also check the failed invoices queue to see if the ingest logged an error. If no error appears, the email may not have been received — confirm you are forwarding to the correct ingest address for your account.

**Can I delete an invoice that was loaded incorrectly?** Yes — go to Billing → Carrier Cost → Invoice Ingest and delete the ingest record. You can only delete an ingest if the invoices within it have not been linked to a bill. If they have been linked, use the adjustments workflow to correct the amounts.

**How does Diversifi handle reseller invoices with multiple carriers on one file?** Diversifi identifies the source as the reseller name and maps each line item to the correct carrier and service based on the data in the file. Per-customer mapping configuration is available if your reseller's file structure varies.
