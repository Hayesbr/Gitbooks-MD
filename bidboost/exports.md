# Exports

BidBoost produces three export types. Each serves a different use case and audience. All exports are Excel (.xlsx) files delivered directly to the prospect or brand.

## Bid Types and Export Availability

The bid type selected at the start of the bid determines what exports are available and which surcharge toggles apply.

**PLD / Shipment File** — Requires a shipment file upload. All three export types are available. This is the only bid type that supports the DAS (Delivery Area Surcharge) toggle — DAS does not appear on SKU or No Data bids. Fuel, residential, and other surcharge toggles are all available.

**SKU** — Requires box dimensions and weights entered per SKU. No shipment file is needed. Net Rates and Blended Rate Card exports are available — Shipment File is not, since there is no historical shipment data to re-rate. The DAS toggle is not available on SKU bids. All other surcharge toggles apply. The Net Rates export follows the SKU-specific format: one tab per rate set + carrier + service, with separate line items per box per rate set.

**No Data** — No file upload or SKU dimensions required. Rates are calculated against market rate benchmarks using a default of 7 lb Zone 4, which the user can override. Net Rates and Blended Rate Card exports are available — Shipment File is not. The DAS toggle is not available. All other surcharge toggles apply. Because there is no shipment data, rates reflect what the 3PL would offer at the selected weight and zone rather than a re-rate of actual shipments.

| Bid type | Net Rates | Blended Rate Card | Shipment File |
|----------|:---------:|:-----------------:|:-------------:|
| PLD / Shipment File | ✓ | ✓ | ✓ |
| SKU | ✓ | ✓ | — |
| No Data | ✓ | ✓ | — |

## Surcharges

Surcharges are additional fees applied on top of base carrier rates. In BidBoost, surcharges are toggled on or off during bid creation and are applied before the markup calculation. The surcharges available depend on the bid type selected — some require actual shipment destination data and are only available on PLD bids.

| Surcharge | PLD / Shipment File | SKU | No Data |
|-----------|:---:|:---:|:---:|
| Fuel | ✓ | ✓ | ✓ |
| Residential | ✓ | ✓ | ✓ |
| Additional Handling / Oversize | ✓ | ✓ | ✓ |
| RAS | ✓ | ✓ | ✓ |
| DAS (Delivery Area Surcharge) | ✓ | — | — |
| EDAS (Extended Delivery Area Surcharge) | ✓ | — | — |

Surcharges shown as — are not available for that bid type and the toggle will be disabled in the platform.

**Fuel** — Applied as a percentage on top of the base rate. Diversifi handles the carrier's weekly fuel surcharge automatically — you enter your negotiated fuel discount percentage in carrier configuration and Diversifi applies it against the carrier's current weekly rate to calculate your effective fuel cost.

**Residential** — Applied when a shipment is delivered to a residential address. On PLD bids this is calculated from the actual destination addresses in the shipment file — only shipments with residential destinations are charged. On SKU and No Data bids a residential surcharge estimate is applied based on the amount configured in your carrier configuration, since no actual destination addresses are available.

**Additional Handling / Oversize** — Applied to packages that exceed standard size or weight thresholds as defined in your carrier configuration. Toggling this on applies it across all qualifying shipments in the bid.

**RAS (Remote Area Surcharge)** — Applied to shipments destined for specific carrier-defined remote areas. Carriers maintain their own lists of qualifying ZIP codes, updated periodically. If none of the shipments in the bid file have destination ZIP codes within the carrier's RAS list, the surcharge will not appear in the export even if the toggle is on — this is expected behavior, not a bug.

**DAS (Delivery Area Surcharge)** — Available on PLD bids only; the toggle is disabled on SKU and No Data bid types. DAS is determined by the destination ZIP code of each shipment. On PLD bids it is applied per shipment where the destination ZIP code falls within the carrier's designated DAS zone. SKU and No Data bids do not contain actual destination ZIP codes, so DAS cannot be calculated on those bid types.

**EDAS (Extended Delivery Area Surcharge)** — Available on PLD bids only; the toggle is disabled on SKU and No Data bid types. EDAS applies to a broader set of extended delivery area ZIP codes beyond the standard DAS coverage area. Like DAS, whether EDAS applies is determined entirely by the destination ZIP code.

**How surcharges interact with markup** — Surcharges are included in the rate calculation before markup is applied:

(Base rate + applicable surcharges) × markup % vs. minimum amount — whichever is greater

This means markups are applied to the full loaded cost including all surcharges, not to the base rate alone.

## Net Rates

**What it is** — A spreadsheet listing every carrier and service a 3PL can offer, with the full weight and zone rate table for each. Rates shown are cost plus markup only — the brand's actual price to use the 3PL for each carrier and service. No underlying cost data is exposed. This export goes directly to the brand, generated by the 3PL sales rep during the bid process.

**When to use it** — When the 3PL wants to show a prospect a complete, transparent picture of every available carrier and service option with full rate visibility.

**Input**

- Carriers and services selected during bid creation
- Cost rates loaded for those carriers on that account
- Markup % or $ amount entered on the markup screen
- Any surcharges toggled on: fuel, residential, RAS, additional handling, oversize, or others
- Bid type (PLD, SKU, or No Data) — determines how rates are sourced

**Rate formula (applies to all bid types)** — For every weight and zone cell, Diversifi calculates the proposed rate as:

(Base rate + applicable surcharges) × markup %, compared against your minimum dollar markup — whichever is greater.

Applicable surcharges include residential, additional handling / oversize, and fuel where toggled on. The larger of the markup-percentage result or your minimum dollar amount becomes the final rate shown in the export.

**Output**

- One tab per carrier/service combination
- Each tab is a weight × zone matrix showing cost + markup rates
- File named: ProspectName_NickName_NetRates
- Tab order: Ground services first, then Air services, grouped by carrier. Example: UPS Ground → UPS Air → FedEx Ground → FedEx Air → UniUni Ground, etc.
- Weights: ounces first, then pounds. All weights are based on DIM weight; if DIM weight does not apply, normal weight is used. DIM weight is never shown as a separate column.
  - DIM weight applies only when a package exceeds 1,728 cubic inches (greater than 1 cubic foot). A package that is exactly 1,728 cubic inches is not subject to DIM weight — actual weight is used.
- Zones: Zone 0 and Zone 9 are removed from the output.

**Multiple rate sets for the same carrier/service** — If you have two rate sets loaded for the same carrier and service, the export shows one tab for that carrier/service. The rate per cell is calculated as the minimum value between the two rate sets, then the greater of that minimum vs. the markup minimum amount. An internal sheet is included with a legend showing which rate set each cell's rate came from. If rate sets have different DIM divisors, DIM weight is calculated per rate set, then per service type (Ground vs. Air); the rate-set-specific carrier config takes priority over the account-level default config.

**Anomaly flagging** — Any cell where the rate is lower than the cell above it (heavier weight, same zone) or lower than the cell to its left (same weight, higher zone) is highlighted. In a normal rate card, rates should increase as weight and zone increase — a decrease in either direction is unexpected and should be reviewed before sending to the prospect.

## SKU Net Rates

**What it is** — A net rates export built from SKU dimensions rather than historical shipment data. Instead of uploading a PLD file, you input box dimensions and weights per SKU. The platform calculates billable weight from those dimensions and runs rates against the 3PL's carrier cost rates and markups.

**When to use it** — When a prospect doesn't have historical shipment data but knows their product dimensions. Common for newer 3PL prospects or brands launching a new product line.

**DIM weight logic** — DIM weight is calculated per rate set, per service type (Ground vs. Air). Each rate set can carry a different DIM divisor for Ground and Air services. DIM weight applies only when a package exceeds 1,728 cubic inches (greater than 1 cubic foot); a package that is exactly 1,728 cubic inches uses actual weight.

**Output** — One tab per rate set + carrier + service combination. Each tab contains separate line items per box, giving full visibility into how that rate set prices each box configuration. When you have multiple rate sets for the same carrier and service — for example two DHL Ground rate sets — each appears as its own tab, distinguished by a 3-digit unique identifier appended to the tab name and printed inside the rate card itself (e.g. DHL Ground 001, DHL Ground 002). Because Excel tab names are capped at 31 characters, longer names are truncated, but the identifier and carrier name are always preserved inside the rate card.

## Blended Rate Card

**What it is** — A carrier-agnostic rate card showing the single cheapest available rate per weight and zone combination, organized by delivery speed tier. No carrier names appear — the 3PL presents these rates as their own pricing. The prospect sees the best available price for each lane and speed without knowing which carrier delivers it.

**When to use it** — When the 3PL wants to act as the carrier themselves and not expose their carrier mix to the prospect. Common for 3PLs with strong negotiated rates who don't want competitors or prospects to know which carriers they use.

**How it works** — The blended card is built directly from the net rate output — rates are not recalculated from scratch. Services are grouped by speed tier, and for each weight/zone cell the system takes the minimum marked-up rate across all qualifying services. Each tier is cumulative: it includes its own services plus any faster service if that faster service produces a cheaper rate.

**Speed tiers** — The speed tier for each service is set automatically based on the service's delivery speed. ("Deferred" services map to Ground Economy.)

**Input** — Same inputs as Net Rates: PLD, SKU, or No Data bid; carrier cost rates; markup settings. If multiple rate sets are selected for the same carrier, the lowest rate across all selected rate sets is used for that carrier before the comparison across carriers.

**Output**

- Five tabs, one per speed tier
- Each tab is a weight × zone matrix — one rate per cell
- Rate per cell = lowest marked-up rate across all qualifying services at that tier or faster

| Tab | Services included |
|-----|-------------------|
| Ground Economy | No delivery guarantee. Minimum across all services — faster services included if cheaper. Broadest tier. |
| Ground (1–5 Day) | Ground-speed services + any faster tier if cheaper. Excludes economy/deferred. |
| 3 Day | 3-day services + 2-day and overnight if cheaper. |
| 2 Day | 2-day services + overnight if cheaper. |
| 1 Day | Overnight/express only. Narrowest tier. |

- No carrier names or service names visible anywhere in the export
- File named: ProspectName_NickName_BlendedRates
- If no services qualify for a speed tier, that tab is empty — no zeros, no errors
- Internally, the winning carrier/service per cell is captured and can be inspected using the Validation View — it is never shown in the export

**Key distinctions**

- *vs. Net Rates:* Net Rates shows every carrier and service with full visibility. Blended collapses everything to one rate per cell with no carrier visibility.
- *vs. Shipment File:* Blended is a rate card (weight/zone matrix). Shipment File re-rates actual shipments row by row.

## Shipment File

**What it is** — A re-rated version of the prospect's actual shipment history. Each shipment in the uploaded file is re-rated against the 3PL's carrier rates and markups, showing exactly what that shipment would have cost under the new pricing. Includes a summary of total potential savings.

**When to use it** — When the prospect has historical shipment data and wants a shipment-by-shipment comparison of their current spend vs. what they would pay under the 3PL's rates. The most compelling sales tool for prospects with meaningful volume.

**Input**

- A shipment file (PLD) — required. No Data bid does not apply to this export type.
- Carrier cost rates and markup settings
- Winning carrier and rate per shipment determined by the bid logic

**Output** — Row-level detail for every re-rated shipment: original carrier and service, re-rated carrier and service, original cost, re-rated cost, markup applied, final quoted amount, zone, weight (actual and billable), and any additional services. Includes a Glossary tab with summary metrics — total shipments analyzed, rated vs. unrated count, current total shipping cost, proposed total shipping cost, and potential annual savings. Shipments that could not be rated appear in a separate Unrated Shipments tab with a specific reason per row. File named: ProspectName_NickName_ShipmentFile.

## Validation View

Diversifi includes a Validation View across all bid export types — SKU Net Rates, Shipment File, and Blended Rate Card exports.

The Validation View lets you inspect exactly how an exported rate was calculated. Select any rate cell to see the underlying inputs and calculations that produced the final value:

- Base rate
- Applied surcharges (fuel, residential, additional handling, DAS, etc.)
- Markup configuration and the calculated markup amount
- Billable and dimensional weight
- Final calculated rate
- Carrier, service, rate set, and zone information
- The underlying rate table values used in the calculation

**Why it's useful** — The Validation View makes every bid result fully auditable, so you can answer questions about a rate without guesswork. Common uses:

- Troubleshooting a customer-reported pricing discrepancy
- Verifying carrier rate imports and rate set configurations
- Confirming markup behavior and surcharge application
- Explaining to a customer exactly how a rate was generated
- Investigating differences between expected and actual export values

**Best practice** — If a rate looks off, use the Validation View first. Many questions trace back to rate configuration, surcharge setup, markup rules, billable weight, or rate-set selection — all visible here — so you can often resolve them without contacting support.
