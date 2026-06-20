# Carrier Configuration

Carrier configuration is where you define the rules, fees, and divisors that determine how shipment costs are calculated for each of your rate sets.

While your cost rates define *what* you pay per shipment, carrier configuration defines *how* those rates are calculated — including dimensional weight logic, fuel surcharges, and accessorial fees. Both must be set up correctly for BidBoost to produce accurate bid outputs.

## How to Access Carrier Configuration

Go to Carriers → Cost Rates and locate the rate set you want to configure. Click the three-dot menu (...) on the far right of that rate set's row and select **Configuration** from the dropdown. This opens the cost rate configuration panel for that specific rate set.

## What Carrier Configuration Does

When Diversifi calculates the cost of a shipment in a bid, it does not just look at the base rate. It also applies a set of carrier-specific rules to determine the true landed cost. For each rate set you can configure:

- **DIM factor** — the divisor used to calculate dimensional weight
- **Fuel surcharge** — the percentage applied on top of the base rate
- **Residential surcharge** — the fee applied to residential deliveries
- **Additional handling** — the fee applied to oversized or irregular packages
- **Remote area surcharge (RAS)** — the fee applied to hard-to-reach ZIP codes
- **Delivery area surcharge (DAS)** — the fee applied to extended delivery areas

## DIM Factor

Dimensional weight (DIM weight) is a pricing method carriers use to account for large, lightweight packages that take up more space than their actual weight would suggest. Instead of charging on physical weight alone, carriers calculate a DIM weight and charge whichever is higher — the actual weight or the DIM weight.

DIM weight = (Length × Width × Height) ÷ DIM factor

The DIM factor is a divisor set by your carrier contract. Common values:

- **139** — standard for USPS and many reseller agreements
- **166** — common for FedEx and UPS retail
- **194** — common for some negotiated FedEx agreements
- **225** — common for some negotiated UPS agreements

Check your carrier contract to confirm the correct DIM factor for each carrier. Using the wrong DIM factor will produce inaccurate rate calculations in every bid.

{% hint style="info" %}
**When DIM weight does not apply:** For USPS, DIM weight only applies to packages over 1 cubic foot (1,728 cubic inches). Packages under 1 cubic foot are rated on actual weight only. Diversifi applies this threshold automatically for USPS — you do not need to configure it manually.
{% endhint %}

## Fuel Surcharge

The fuel surcharge is a percentage added on top of the base rate to account for carrier fuel costs. This percentage fluctuates and is typically updated by carriers weekly or monthly. Rather than requiring you to update it in every rate set each week, Diversifi handles the weekly carrier fuel surcharge automatically.

Enter your negotiated fuel discount percentage in the carrier configuration settings. Diversifi applies your discount against the carrier's current weekly fuel surcharge to calculate your effective fuel cost. If you do not have a negotiated discount, your fuel surcharge will be the carrier's published rate.

{% hint style="info" %}
The fuel surcharge applies to the base rate **before** your markup is calculated:
(Base rate + Fuel surcharge amount) × Markup percentage = Proposed rate
{% endhint %}

## Accessorial Fees

Enter the following fees at the costs you pay **before** fuel is applied. Diversifi applies fuel logic separately based on the carrier's weekly rate and your configured discount.

- **Delivery Area Surcharge (DAS)** — Applied to shipments destined for extended delivery area ZIP codes maintained by each carrier. Only shipments with destination ZIP codes that fall within the carrier's defined DAS list trigger this fee.
- **Extended Delivery Area Surcharge (EDAS)** — A subset of DAS that applies to a further extended set of ZIP codes beyond the standard DAS coverage area.
- **Remote Area Surcharge (RAS)** — Applied to shipments destined for the most remote and difficult-to-service ZIP codes. RAS affects a smaller subset of ZIP codes than DAS and appears less frequently in bid exports. If none of the prospect's shipments go to qualifying ZIP codes, RAS will not appear in the export even if configured.
- **Residential Surcharge** — Applied to shipments delivered to residential addresses. If a significant portion of the prospect's shipments are residential, this fee can have a meaningful impact on the proposed rate.
- **Additional Handling** — Applied to packages that exceed certain size or weight thresholds. Common triggers include exceeding maximum length, not being in a corrugated box, or having an irregular shape.
- **Oversize Fee** — Applied to packages that exceed the carrier's defined oversize dimensions or weight limits.

Once all values are entered, click Save.

## Connecting Carrier Accounts

In addition to configuring pricing parameters, you can connect your live carrier accounts to Diversifi through the Integrations section. Connecting a carrier account allows Diversifi to pull in your actual carrier invoices for billing reconciliation.

Carrier configuration and carrier account connections are two separate things:

- **Carrier configuration** — defines how rates are calculated in bids
- **Carrier account connection** — links your live account for invoice ingestion and billing

You can run bids without connecting a carrier account as long as your cost rates and carrier configuration are set up. The carrier account connection is required for billing and reconciliation features. See [Carrier Integrations](../integrations/carrier-integrations.md) for instructions.

## Saving Your Configuration

Configuration is saved at the rate set level — each rate set maintains its own independent configuration. This means you can have different DIM factors, fuel discounts, and accessorial fees for each rate set, even for the same carrier.

## Common Questions

**Where does carrier configuration live?** Configuration is accessed via the three-dot menu on each individual rate set in Carriers → Cost Rates. It is not a separate page — it lives directly on the rate set.

**Do I need to configure every rate set?** Yes — every rate set you plan to include in a bid must have a DIM factor entered at minimum. Without it, the platform cannot calculate dimensional weight and bids will produce inaccurate results.

**Why is RAS not showing in my export?** If RAS is configured but not appearing, it means none of the destination ZIP codes in the prospect's shipment file fall within the carrier's RAS ZIP code list. This is not a bug — it means the prospect's shipments do not include any remote area destinations for that carrier.

**Can I have different configurations for different rate sets of the same carrier?** Yes — each rate set has its own configuration panel, so you can apply different DIM factors, fuel discounts, and accessorial fees to each rate set independently, even for the same carrier.

**How often do I need to update carrier configuration?** The fuel discount only needs to be updated if your negotiated fuel discount changes — Diversifi handles the weekly carrier fuel surcharge automatically. DIM factors and accessorial fees typically only change when you renegotiate your carrier contract.
