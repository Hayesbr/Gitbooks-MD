# Carrier Reconciliation

Carrier reconciliation is the process of comparing what your WMS quoted as the shipping cost against what the carrier actually charged on their invoice. The difference between these two numbers — the variance — is what reconciliation captures and resolves. Understanding reconciliation is one of the most important parts of running a profitable 3PL, because unresolved variances mean either you are overcharging your customers or absorbing costs that should be passed through.

## Why Reconciliation Exists

When a 3PL quotes a shipping rate to their customer, they are working from an estimate — the WMS rate shop or the contracted rate loaded in Diversifi. The actual carrier invoice that arrives days or weeks later reflects what the carrier actually charged, which can differ from the quote for a number of reasons:

- Address corrections applied after the shipment was picked up
- Dimensional weight adjustments where the carrier re-weighed the package
- Fuel surcharge fluctuations between the quote date and the invoice date
- Residential or delivery area surcharges not captured in the original quote
- Late delivery credits or carrier adjustments
- Rate changes that took effect between the quote and the invoice

Reconciliation is how you close the gap between what was quoted, what was billed to your customer, and what the carrier actually charged you.

## How Reconciliation Works in Diversifi

Reconciliation happens automatically as carrier invoices come in through invoice ingest. When an invoice is received, Diversifi matches each line item to the corresponding shipment record using the tracking number. For each matched shipment, Diversifi calculates:

- **Quoted amount** — what the WMS estimated the shipment would cost
- **Actual amount** — what the carrier charged on the invoice
- **Variance** — the difference between the two

If the actual amount is higher than the quoted amount, the variance is positive (the carrier charged more than expected). If it is lower, the variance is negative. These variances flow into the Adjustments section of the next bill for the affected customer, including the applicable markup so your margin is maintained on the corrected charge.

## Viewing Reconciliation

Go to Billing → Carrier Cost → Reconciliation to see the reconciliation view for your account. It shows all shipments that have been matched against a carrier invoice, organized by carrier and billing period, with the tracking number, quoted amount, actual amount, variance, and reconciliation status for each.

**Reconciliation statuses:**

- **Matched** — the shipment has a carrier invoice line item and the amounts have been compared. Variance is calculated and will flow into the next bill as an adjustment if applicable.
- **Unmatched — invoice** — a carrier invoice line item exists but no corresponding WMS shipment record was found.
- **Unmatched — shipment** — a WMS shipment record exists but no carrier invoice line item has arrived yet. This is normal for recent shipments.
- **Disputed** — the variance on this shipment has been flagged for review. No adjustment is created until the dispute is resolved.

## Unmatched Records

Unmatched records are the most common reconciliation issue and usually resolve themselves as invoices come in or WMS syncs catch up. Some require manual investigation.

**Unmatched invoice — common causes:**

- The tracking number on the carrier invoice uses a different format than the WMS recorded (e.g. a leading-zero difference or a carrier-specific prefix)
- The shipment was processed through a carrier account not connected to Diversifi
- The invoice line item is for a fee type not associated with a specific tracking number, such as a fuel surcharge billed at the account level

**Unmatched shipment — common causes:**

- The carrier invoice for this period has not yet arrived or been ingested
- The shipment was voided or cancelled after it synced from the WMS but before the carrier invoice arrived
- The carrier invoiced on a different cycle than expected

To investigate, click into the record from the reconciliation page. You'll see the full shipment or invoice detail and a notes field where you can log your investigation. If the record can't be matched automatically, you can manually link it to the correct counterpart or mark it as resolved with a note.

## Adjustments from Reconciliation

When a matched shipment has a variance, the adjustment flows into the next billing period automatically — you do not need to create adjustments manually. Adjustments appear in the Adjustments section of the bill, showing the tracking number, the original billed amount, the actual carrier cost, the adjustment amount (including markup), and a note indicating it originated from carrier reconciliation. Your customer sees the adjustment as a line item on their next bill, with a description explaining it is a carrier cost correction so the charge is transparent and auditable.

## Reconciliation and Multi-Shipment Logic

If multi-shipment logic is enabled, reconciliation accounts for the redistributed costs rather than the original WMS costs. Diversifi compares the redistributed per-package cost against the carrier invoice line item for each tracking number rather than the raw WMS amount. This means that for multi-shipment orders, the reconciliation variance will typically be much smaller once multi-shipment logic is enabled, because the redistributed cost is a more accurate representation of the true per-package cost. See [Multi-Shipment Logic](multi-shipment-logic.md) for more detail.

## Extensiv and Reconciliation

If your WMS is Extensiv, there are some important limitations to be aware of. Extensiv does not consistently provide a quoted shipping cost through its standard API, which means the quoted amount in reconciliation may be blank or inaccurate for Extensiv accounts — making traditional variance reconciliation difficult.

The recommended approach for Extensiv accounts is to configure billing to use **carrier invoice by invoice date** rather than WMS shipments. In this configuration, Diversifi bills directly off the carrier invoice actuals rather than WMS quotes, which eliminates the reconciliation gap entirely for the core billing workflow. If you need full quoted cost reconciliation through Extensiv, you will need to enable Extensiv's billing module and provide the separate API credentials. Contact your Diversifi account manager to discuss this setup.

## Carrier Credits and Disputes

If a carrier applies a credit to your account — for example a late delivery credit or a billing error correction — it appears on the carrier invoice as a negative line item. Diversifi ingests these credits and they appear in the reconciliation view as negative variances. If the credit applies to a shipment already billed to your customer, it flows into the Adjustments section of the next bill as a negative adjustment, crediting the customer back for their share.

**Disputing a carrier charge** — If you believe a carrier charged incorrectly for a shipment, flag it in the reconciliation view by setting the status to Disputed. A disputed shipment will not generate an adjustment until the dispute is resolved. Once you've resolved the issue with the carrier, update the status and the correct variance will flow through on the next billing period.

## Common Questions

**How long does it take for carrier invoices to appear in reconciliation?** It depends on the carrier and ingestion method. Carrier integrations via Trackstar typically pull invoices within 24 to 48 hours of the invoice being available on the carrier portal. Email ingest processes within a few minutes of receipt. Manual uploads are available immediately.

**Why do some shipments have large variances even though nothing seems wrong?** Large variances on multi-shipment orders are almost always caused by how the WMS records costs across multiple tracking numbers, not an actual billing error. Enabling multi-shipment logic will normalize these costs and significantly reduce apparent variances.

**Can I export the reconciliation data?** Yes — go to the reconciliation page and click Export. The export includes all matched and unmatched records for the selected period with full detail on quoted amounts, actual amounts, and variances. Both internal and summary export formats are available.

**What happens to unmatched records at the end of a billing period?** Unmatched records remain open until they are resolved — they do not automatically close at the end of a period. Diversifi surfaces them on the reconciliation page so your team can investigate before the next bill is generated.

**How far back does reconciliation go?** Diversifi reconciles against all carrier invoices that have been ingested, regardless of age. If an invoice arrives months after the original shipment, it will still be matched against the WMS record and the variance will flow into the next bill as an adjustment.

**Can I prevent adjustments from appearing on customer bills?** No — adjustments are a core part of the billing workflow and cannot be suppressed. They ensure your customers are billed accurately and that you are not absorbing carrier cost differences silently. To minimize large adjustments, ensure invoices are ingested promptly and enable multi-shipment logic where applicable.
