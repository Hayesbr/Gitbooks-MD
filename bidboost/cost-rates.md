# Cost Rates

Cost rates are your negotiated carrier rates — the actual amounts you pay per shipment for each carrier, service, weight, and zone combination.

Loading your cost rates correctly is the most important setup step in BidBoost. Every bid you run uses these rates as the foundation for calculating what you will propose to your prospect.

## What Cost Rates Are

When you negotiate a contract with a carrier like FedEx, UPS, or USPS, you receive a rate sheet showing what you pay per pound/oz per zone for each service. These are your cost rates. They are different from the published retail rates anyone can see on a carrier's website — your negotiated rates reflect the volume discounts and contract terms your 3PL has secured.

Diversifi uses your cost rates to:

- Calculate the base rate for every shipment in a bid
- Apply your markup on top to produce the proposed rate for the prospect
- Compare your rates against market data to show how competitive your pricing is

Your actual cost rates are never visible to the prospect. They only ever see the proposed rate after your markup has been applied.

## Understanding Rate Sets

Cost rates in Diversifi are organized into **Rate Sets**. A Rate Set is an independent pricing structure for a specific carrier and service combination. Every time you enter rates for a carrier you are creating a Rate Set, and you can have multiple Rate Sets for the same carrier.

**Why would you have more than one Rate Set for the same carrier?** Many 3PLs operate under several different negotiated agreements for the same carrier depending on how they access those rates. Common examples include:

- A direct contract negotiated with FedEx or UPS
- A reseller agreement through a third party
- Blanket rates accessed through a rate shopping tool like Shopify Shipping

Each agreement will have different base rates, surcharge structures, and margin expectations. Keeping them as separate Rate Sets ensures the pricing, markups, and bid outputs tied to each agreement stay accurate and don't bleed into each other. Each Rate Set maintains its own base transportation rates, DIM factor, surcharge configurations, markup strategies, and profitability targets.

## Naming Your Rate Sets — Nicknames Matter

Because you may have several Rate Sets for the same carrier, the nickname you give each Rate Set is how you will identify and select them throughout the platform. Use names that reflect the agreement type, the warehouse they are associated with, or the volume tier they apply to:

- **By volume tier** — "FedEx Ground - Tier 1 (1k–5k monthly)" and "FedEx Ground - Tier 2 (5k–10k monthly)"
- **By origin location** — "DHL eCommerce - California Hub" and "DHL eCommerce - Indiana Hub"
- **By discount structure** — "UPS 2nd Day Air - Standard Discount" and "UPS 2nd Day Air - VIP Account"

Avoid generic names like "FedEx 1" or "FedEx 2" — these become confusing quickly when you have multiple rate sets across multiple carriers.

## Loading Your Cost Rates

Go to Carriers → Cost Rates from the left sidebar and click Add New Cost Rates in the top right corner.

1. **Select carrier details** — Choose your carrier (e.g. FedEx), the associated carrier account, and the provider (e.g. EasyPost).
2. **Assign a nickname** — Give the rate set a descriptive name such as "FedEx Home Delivery - Standard." See the nickname guidance above.
3. **Set dates and warehouses** — Define the effective date range for these rates and assign the relevant warehouses. The platform will use these rates for bids during the specified date range and for the assigned warehouses only.
4. **Add services** — Click + Add Service to select the specific shipping service level from the dropdown — for example FedEx Home Delivery. Repeat for each service you want to include.
5. **Paste your rates** — Click the Paste Rates button and paste your pricing matrix directly from your carrier rate spreadsheet into the system grid. Rows are weight breaks; columns are zones.
6. **Submit** — Click Submit to save the new rate set.

A few things to know about the rate grid:

- **Zone 1 and sub-1 lb pricing** — Some carriers do not offer Zone 1 or sub-1 lb pricing tiers. If yours doesn't, you can start your pricing at the Zone 2 / 1 lb cell. If a shipment maps to Zone 1 or is under 1 lb, the platform automatically defaults to the Zone 2 / 1 lb rate.
- **Ounces first, then pounds** — Enter ounce-based pricing rows first if your carrier supports them, then move to pound-based rows.

## Editing Existing Cost Rates

Go to Carriers → Cost Rates and locate the rate set you want to update. Click the three-dot menu (...) on the far right of that rate set's row and select **Edit** (not Configuration). This opens the rate set editor where you can update the warehouses the rate set is assigned to and edit the rates themselves. Click Submit or Save to apply your changes.

## Managing Multiple Rate Sets

If you have more than one rate set for the same carrier — for example different FedEx rates for different warehouses, volume tiers, or discount structures — each is added as a separate entry with its own unique nickname. To view all rate sets, go to Carriers → Cost Rates and use the search or filter to find rate sets by carrier name or nickname.

**Deactivating a rate set** — If a rate set is no longer in use, you can deactivate it rather than deleting it. Deactivated rate sets will not appear as options in the bid flow but are retained for historical reference and billing reconciliation on past shipments.

**When multiple rate sets apply to the same carrier in a bid:**

- On the **Net Rate** export — all selected rate sets are included, one tab per rate set
- On the **Blended Rate** export — the cheapest rate per weight and zone combination is used across all selected rate sets for that carrier

## Assigning Rate Sets to Warehouses

Rate sets can be assigned to specific warehouses so that when a sales rep selects a warehouse in a bid, only the rate sets assigned to that warehouse are available. This prevents a rep from accidentally using California rates on a bid that should be priced off Indiana rates. There are two ways to assign:

- **From the rate set** — Go to Carriers → Cost Rates, locate the rate set, click the three-dot menu (...), select Edit, choose which warehouses this rate set applies to, and click Submit.
- **From the warehouse** — Go to Data → Warehouses, select the warehouse, and assign the relevant rate sets from the warehouse configuration panel.

If a warehouse has no rate sets assigned, all rate sets on the account will be available — the warehouse assignment acts as a filter, not a hard restriction. See [Warehouses](warehouses.md) for more.

## Warehouse-Level Additional Fees

Some 3PLs charge fees on top of carrier base rates that are specific to a warehouse — a linehaul fee for a regional carrier that injects at a hub, a commission on a reseller rate, or a flat handling charge. The warehouse-level additional fee configuration lets you define these fees per warehouse and per rate set so they're automatically included in bid calculations and exports.

**Where to configure it** — Warehouse-level additional fees can be configured in two places, and changes sync automatically between them:

- **Cost Rates page** — when a warehouse is enabled on a rate set, a Fees option appears next to it showing the count of active fees. Click to manage fees for that warehouse.
- **Warehouse page** — navigate to the warehouse directly and find the same fee configuration under the associated rate set.

**Adding a fee** — Each fee requires:

- **Name** — a label for your reference (e.g. "Linehaul Fee", "Platform Commission")
- **Type** — either a **Flat rate** (a fixed dollar amount per shipment) or a **Commission** (a percentage of the carrier base rate)
- **Amount** — the dollar amount or percentage value
- **Apply before or after markup** — whether the fee is included in the base cost before your markup percentage is applied, or added on top after markup

**Order of application** — When multiple fees are configured, the order they appear in the list determines the order they're applied (drag to reorder). All "before markup" fees are applied first in order, then markup is calculated, then all "after markup" fees are applied in order. For example:

1. Linehaul Fee — $5.00 flat — before markup
2. Markup — 20%
3. Platform Commission — 3% — after markup

Here the linehaul fee is added to the base rate first, then the 20% markup is applied to the combined amount, then the 3% commission is applied to the marked-up total.

**How fees appear in bids** — Once configured, these fees flow through automatically whenever that warehouse and rate set are used: as individual line items in the bid breakdown / Rate Review, in the shipment file export calculation columns, in the final quoted rate on the Net Rates export, and in the Blended Rate Card calculation.

**Things to know:**

- A warehouse can have multiple fees — there is no limit.
- Fee names are for your reference and appear in the bid breakdown, so choose names that are meaningful to your team.
- Fees are specific to the warehouse and rate set combination — the same carrier on two different warehouses can have different fees on each.
- If no fees are configured for a warehouse, the bid calculation works exactly as before — this feature only activates when fees are added.

{% hint style="info" %}
Warehouse-level additional fees currently apply to PLD (shipment file) bids only. SKU and No Data bid types are not currently supported.
{% endhint %}

## Carrier Configuration

Once your cost rates are added, you need to configure the carrier-specific rules, fees, and divisors that apply to that rate set — DIM factor, fuel discount, and accessorial fees. Carrier configuration lives directly on each individual rate set (via the three-dot menu → Configuration), not on a separate screen. See [Carrier Configuration](carrier-configuration.md) for full detail.

## Keeping Rates Up to Date

Carrier rates typically change annually. When you receive new rates from a carrier:

1. Go to Carriers → Cost Rates
2. Add a new rate set with the new effective date range
3. The platform will automatically use the correct rate set based on the bid date

Do not delete old rate sets — keep them for historical reference and accurate billing reconciliation on past shipments.

## Common Questions

**Can I paste rates directly from my carrier's spreadsheet?** Yes — use the Paste Rates button to paste your pricing matrix directly from Excel or your carrier's rate file. This is the fastest way to enter rates and avoids manual entry errors.

**What if my carrier doesn't have Zone 1 or sub-1 lb pricing?** Start your pricing at the Zone 2 / 1 lb cell. The platform automatically defaults to Zone 2 / 1 lb rates for any shipment that maps to Zone 1 or weighs under 1 lb.

**Why do I need to enter a DIM factor for every rate set?** The DIM factor is required for the platform to calculate dimensional weight on shipments in a bid. Without it, the platform cannot determine whether a package should be rated on actual weight or DIM weight, which produces inaccurate rates. Always populate this field before saving your configuration.

**Can I upload rates from a CSV or Excel file directly?** Not currently — rates are entered using the Paste Rates button, which lets you paste your matrix from a spreadsheet. Full CSV import is not currently supported due to the wide variation in how carrier rate sheets are formatted.

**How do I apply different configurations to different rate sets for the same carrier?** Each rate set has its own configuration panel accessed via the three-dot menu. This means you can have different DIM factors, fuel discounts, and accessorial fees for each rate set, even for the same carrier — which is why clear nicknames matter.
