# Billing Overview

Diversifi Billing automates the most time-consuming part of running a 3PL — turning carrier invoices, WMS shipment data, and your pricing rules into accurate, reviewable customer bills. What used to take 20 to 30 hours of manual spreadsheet work per billing cycle can be completed in minutes.

## How Billing Works

Diversifi Billing has two distinct sides that work together:

- **Customer Billing** — how you charge your customers. This is where you create billing cycles, apply your pricing rules, review bills, and send them out.
- **Carrier Cost** — how carriers charge you. This is where your carrier invoices come in through invoice ingest and are reconciled against what you quoted your customers.

The sidebar in Diversifi separates these two mental models clearly. Everything under Customer Billing is about what you send to your customers; everything under Carrier Cost is about what you owe your carriers.

## The Billing Flow

Every bill follows the same flow from start to finish:

1. **Set up your billing cycle** — A cycle defines the rules for how a group of customers gets billed: the billing type, the cadence, and whether billing is based on carrier invoice date or ship date.
2. **Create a period** — A period is a specific billing window within a cycle, for example the week of May 1 through May 7. Each period generates bills for all customers in that cycle.
3. **Ingest your carrier invoices** — Connect your carrier accounts or set up email ingest so invoices flow in automatically. Diversifi matches invoice line items against your WMS shipment data.
4. **Apply your billing rules** — Your pricing rules (pick and pack fees, order fees, markups, handling fees, discounts) are applied automatically to generate each customer's bill.
5. **Review and approve** — Each bill is broken into four sections for review: Parcel Charges, Order Charges, Adjustments, and Other Fees. Your team reviews each section, checks the numbers, and marks the bill as approved.
6. **Export and send** — Once approved, export the bill in the format that works for your customer — internal-facing with full rule and margin detail, or customer-facing with clean charge summaries. After a bill is marked as sent it cannot be modified.

## The Four Bill Sections

Every bill is organized into four logical sections that match how 3PL billing actually works:

- **Parcel Charges** — All fees tied to individual shipments at the tracking number level: the quoted amount, actual carrier cost, variance, markup, pick and pack fees, packaging fees, and handling fees. If it happened at the package level, it shows up here.
- **Order Charges** — Fees that apply at the order level regardless of how many packages went out. The most common example is an order processing fee — a flat fee per order that does not change based on box count. Tiered order fees also show up here.
- **Adjustments** — The result of carrier reconciliation. When a carrier invoice comes in after a billing period has closed, or when the actual carrier cost differs from the quoted amount, those differences are captured as adjustments in the next bill, including the markup applied to the adjustment.
- **Other Fees** — A catch-all for fees that do not fit the parcel or order level: storage fees, monthly technology fees, account management fees, and ad hoc manual adjustments or discounts. You can add fees here directly if a rule did not apply correctly.

## Billing Types

When creating a billing cycle you choose what type of activity to bill for:

- **Transportation only** — carrier shipping costs only
- **Fulfillment / warehouse fees only** — pick and pack, storage, receiving, and other fulfillment fees only
- **Both** — transportation and fulfillment together

This matters because many 3PLs bill transportation weekly and warehousing monthly. You can create separate cycles for each or combine them in one.

## What Billing Is Based On

When creating a cycle you choose what data source drives the billing:

- **Carrier invoice — by invoice date (recommended)** — Bill based on when the carrier invoice was received. This is the cleanest option because you are billing on confirmed actual carrier data rather than estimates. When a new invoice arrives, everything on that invoice gets billed in the current period.
- **Carrier invoice — by ship date** — Bill based on when the shipment was picked up rather than when the invoice arrived. This can create ambiguity because invoices sometimes arrive weeks after the ship date, pulling historical charges into current periods. Use this only if your contracts require ship date billing.
- **WMS shipments — by ship date** — Bill based on the quoted cost from your WMS rather than the actual carrier invoice. Used when you are billing on rate shop estimates rather than reconciled actuals.

Our recommendation is **carrier invoice by invoice date**. It is the cleanest method and produces the least variance and confusion for your customers.

## Rules Drive the Numbers

Billing rules tell Diversifi how to calculate each fee on each bill. Rules define the conditions and the output — for example "if a parcel is picked and packed, apply a $0.50 pick fee per unit" or "if an order has more than 3 items, apply a tiered order processing fee."

Rules are applied automatically when a bill is generated. If rules change, you can regenerate any bill at any time to apply the updated rules — or regenerate all bills in a cycle at once. See [Billing Rules](billing-rules.md) for full detail.

## Reviewing and Approving Bills

Diversifi includes a built-in review and audit trail. Each of the four bill sections can be checked off individually as your team reviews them. When all four sections are marked reviewed, the bill status moves to Needs Approval. (You can also mark all sections reviewed at once from the bill header.)

Every review action is logged — Diversifi records who reviewed which section and when. This audit trail is visible on the bill and ensures accountability across your billing team. Once a bill is approved and sent it is locked; any subsequent corrections appear as adjustments on the next bill. See [Bill Review](bill-review.md) for full detail.

## Exporting Bills

Every bill can be exported in two formats:

- **Internal export** — includes the full detail behind every charge: rule names applied, markup amounts, quoted vs. actual costs, and shipment margin. Used by the 3PL team to validate billing math before sending to the customer.
- **Customer-facing export** — a clean version with charge descriptions and amounts only. No internal cost data, no markup visibility, no rule names. Safe to send directly to the customer.

Both exports are available for all four bill sections. You can also export all bills in a cycle at once as a zip folder with each customer's file named after the customer. See [Billing Exports](exports.md) for full detail.

## Multi-Shipment Orders

When a customer orders multiple products that ship in more than one box, different WMS systems handle the shipping cost differently — some put the total on the first tracking number only, some put the total on every tracking number, and some list only the first tracking number with the combined total. This creates large apparent variances when Diversifi reconciles quoted costs against actual carrier invoice costs.

Diversifi normalizes these costs automatically using weighted-average cost logic. When multi-shipment logic is enabled, Diversifi identifies all parcels in the same order, sums the total shipping cost, and distributes it across each parcel proportionally based on weight. Adjusted costs are marked with an indicator so your team can see which line items have been normalized. See [Multi-Shipment Logic](multi-shipment-logic.md) for full detail.

## Common Questions

**What is the difference between Customer Billing and Carrier Cost?** Customer Billing is what you charge your customers (outbound). Carrier Cost is what carriers charge you (inbound). Both live in the Billing section but serve different purposes.

**Can I change a bill after it has been sent?** No — once a bill is sent externally it is locked. Any corrections need to be made as adjustments on the next billing period.

**What happens if a carrier invoice arrives after a billing period has closed?** It appears as an adjustment in the next bill. The Adjustments section captures all late invoices and the delta between what was originally billed and the actual carrier cost.

**Can I regenerate a bill if I update my rules?** Yes — you can regenerate any individual bill or all bills in a cycle at once from the bills page. Regenerating applies your current rules to the existing data and recalculates all fees.

**What is the best billing method to recommend to customers?** Carrier invoice by invoice date. It is the cleanest method, produces the least ambiguity, and ensures you are billing on confirmed actuals rather than estimates.

**Can I export bills in bulk?** Yes — select multiple bills and export them all at once. Choose to download individually or as a named zip folder, with each file named after the customer.
