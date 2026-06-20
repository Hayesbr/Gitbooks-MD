# FAQ

Quick answers to the most common questions across Diversifi. For detail, follow the link to the full article.

## Getting Started

**How long does setup take?** Most 3PLs are fully set up within their first week. The [Getting Started](getting-started.md) guide walks through each step.

**What user roles are available?** Three: Owner (full access including user management and settings), Manager (full access to all features), and Regular (can run bids, manage billing records, and view reports, but cannot manage users or integrations).

**Which warehouse management systems are supported?** Extensiv, ShipHero, and ShipStation. See [WMS Integrations](integrations/wms-integrations.md).

## BidBoost

**What are the three bid types?** PLD (re-rates an uploaded shipment file — most accurate), SKU (rates your product dimensions), and No Data (a market rate comparison with no prospect data). See the [BidBoost Overview](bidboost/README.md).

**Why is a carrier not showing up in my bid?** Either the carrier doesn't have cost rates loaded, or the rate set isn't assigned to the selected warehouse. Check Carriers → Cost Rates.

**Why does my export show different rates than my cost rates?** Usually a surcharge toggle is on or a markup is applied. Run the bid again at 0% markup with surcharges off and compare to your cost sheet.

**What's the difference between the export types?** Net Rates shows every carrier and service with full rate visibility; Blended Rate Card collapses everything to one cheapest rate per cell with no carrier names; Shipment File re-rates the prospect's actual shipments row by row. See [Exports](bidboost/exports.md).

**How is dimensional weight calculated?** DIM weight = (Length × Width × Height) ÷ DIM factor. For USPS, DIM weight only applies to packages over 1 cubic foot. See [Carrier Configuration](bidboost/carrier-configuration.md).

## Billing

**What's the difference between Customer Billing and Carrier Cost?** Customer Billing is what you charge your customers (outbound). Carrier Cost is what carriers charge you (inbound).

**What billing method do you recommend?** Carrier invoice by invoice date — it's the cleanest method and produces the least variance. See [Cycles and Periods](billing/cycles-and-periods.md).

**Can I change a bill after it has been sent?** No — once sent, a bill is locked. Corrections appear as adjustments on the next billing period.

**Can more than one billing rule apply to the same shipment?** Yes — all matching rules apply. Markups sum, fees stack as separate line items, and discounts apply based on stackability. See [Billing Rules](billing/billing-rules.md).

**What happens if a carrier invoice arrives after a period has closed?** It's captured as an adjustment in the next bill, showing the delta between what was originally billed and the actual carrier cost. See [Carrier Reconciliation](billing/carrier-reconciliation.md).

**Why do some shipments show large variances even when nothing's wrong?** Almost always how the WMS records costs on multi-shipment orders. Enabling [Multi-Shipment Logic](billing/multi-shipment-logic.md) normalizes these costs and reduces apparent variance.

## Integrations

**Do I need a WMS integration to use billing?** Yes — billing rules can't be created until at least one active WMS integration is connected, because rules are evaluated against your order and shipment data.

**How do carrier invoices get into Diversifi?** Three ways: carrier integration via Trackstar (recommended), email ingest, or manual upload. Don't use both an integration and email ingest for the same carrier — that creates duplicates. See [Invoice Ingest](billing/invoice-ingest.md).

**Why are my Extensiv reconciliation numbers off?** Extensiv doesn't consistently provide a quoted cost through its standard API. For Extensiv accounts we recommend billing by carrier invoice date. See [Carrier Reconciliation](billing/carrier-reconciliation.md).

## Still Need Help?

Use the search bar at the top of any page, or see [Support](support.md) to reach your account manager.
