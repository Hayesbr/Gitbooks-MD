# Billing Rule Guide

Your complete guide to building the 10 standard billing rules.

Billing rules are how Diversifi calculates every fee on every bill — automatically. Instead of building charges by hand in a spreadsheet each cycle, you set up a rule once and Diversifi applies it every time a bill is generated. The 10 standard rules in this guide cover roughly 80% of the billing structures used across 3PLs. Start here, get comfortable, then layer custom rules on top for the last 20%. Each rule includes plain-English setup steps, a ready-to-use Owlfred prompt, and a worked example.

{% hint style="info" %}
**Before you start:** A WMS integration is required before you can create billing rules. Rules read your order and shipment data, so the platform needs at least one active WMS connection first. See [WMS Integrations](../integrations/wms-integrations.md).
{% endhint %}

## Quick Reference — The 10 Standard Rules

| # | Rule | Category |
|---|------|----------|
| 1 | Standard Unit Pick Fee | Pick & Pack |
| 2 | Pick Fee Tiered by Volume | Pick & Pack |
| 3 | Order Processing Fee | Orders |
| 4 | Carrier Markup (Flat Dollar or Percentage) | Carrier |
| 5 | Third-Party Freight Handling Fee | Carrier |
| 6 | Carrier Rate Sheet (Weight × Zone) | Carrier |
| 7 | Inbound Receiving Fee | Receiving |
| 8 | Returns Processing Fee | Returns |
| 9 | Packaging Materials Fee | Packaging |
| 10 | Monthly Recurring Fee | Account |

## How Billing Rules Work

Every rule answers two questions: *when* should a charge apply, and *what* is the charge? For example: "When a unit is picked, charge $0.50 per unit," or "When an order ships, add a flat $2.00 processing fee." Every rule is built from the same parts:

- **Trigger** — the event the rule reacts to: a unit picked, an order fulfilled, a return processed, a billing period opening.
- **Data set** — the type of activity the rule looks at (parcels, orders, returns, receipts). Which data sets are available depends on your WMS integration.
- **Filter / Conditions** — tests that must be true for the rule to fire, combined with AND/OR (e.g., "Fulfillment Status = Fulfilled"). A rule with no conditions applies to every matching event. If a condition fails, the rule is skipped entirely.
- **Branches** — variations inside one rule that apply different rates depending on the event: one branch per carrier, per package type, per warehouse. Rules branch **one level deep** — a branch cannot contain another branch.
- **Sheets & Pivots** — a faster way to build many branches at once from a table, or to price on two dimensions (like weight × zone) in a single rule. See the next section.
- **Action** — what gets charged when the rule matches: a **Markup** (adds margin on top of carrier cost), a **Fee** (a charge like a pick or handling fee), or a **Discount** (a reduction, e.g., volume or loyalty).
- **Customer scope** — who the rule applies to: All Customers, an include list, or an exclude list. Keep one standard rule set and carve out exceptions per customer.
- **Priority** — the order rules are evaluated in. Lower number = higher priority (priority 1 runs before priority 100). Use lower numbers for rules that should take precedence.
- **Owlfred** — the built-in AI assistant. Describe the rule in plain English and Owlfred builds it — and it can read rate tables pasted straight from a spreadsheet, columns, rows, and all.

## How Multiple Rules Combine

More than one rule can — and usually will — apply to the same shipment. That's the intended design: you layer simple rules instead of building one giant rule for every scenario.

- **Markups add together.** A 10% markup + a 5% markup + a $2.00 flat markup = (cost basis × 15%) + $2.00. Multipliers are converted to a markup amount and summed, not compounded.
- **Fees stack as separate line items.** A fuel surcharge, a residential fee, and a handling fee can all hit the same shipment, and each appears on the bill on its own line.
- **Discounts respect stackability.** Stackable discounts all apply together. If a non-stackable discount matches, only one applies — the highest-priority one.

**Calculation order:** Diversifi first totals all matching markups (or applies your account's default markup if none match), adds that to the cost basis for a subtotal, then calculates fees (on the cost basis) and discounts (on the subtotal) as separate tracked amounts.

{% hint style="info" %}
**Safety net:** If no markup rule matches a shipment, your account's default markup applies — so a shipment is never billed at raw cost. Set a sensible default on your account.
{% endhint %}

**Full audit trail** — Every bill line item records which rules matched and what each contributed, so you can always see exactly why a charge is what it is. The internal bill export lists the rule names applied to each charge.

**Changing rules after bills exist** — Rules apply automatically when a bill is generated. If you change a rule after bills already exist, regenerate the affected bills to apply the update — individually or all bills in a period at once. Regenerating recalculates fees using your current rules against the same underlying data; it doesn't change shipment or invoice data, and it can't be done on a bill that has already been sent.

## Sheets & Pivots — Build Many Branches at Once

If you want a different rate for each of your carriers (or customers, or package types), you no longer have to add branches one at a time. The **Add Sheet** option in the rule builder turns that into a table you can fill in — or paste straight from Excel.

### Sheet — one field, many values

A Sheet prices a single field across all of its values (for example, a carrier markup).

- Pick the field (e.g., Carrier), and the sheet becomes a two-column table: one row per value, one column for your rate.
- Click **Populate** to auto-fill a row for every value in your account — all your carriers, all your customers, whatever the field is. No retyping names.
- Enter your rates. Type them, paste a column straight from Excel, or select a range of cells and fill them with the keyboard.
- Set the **Action** template once (e.g., Apply Markup, Percentage of cost basis). Every row uses that action; each row's number is the amount for that value.
- **Save.** The sheet expands into branches automatically — one branch per filled row. Any row you left empty is deleted on save, so only the rates you actually set become rules.

### Pivot — two fields, rows × columns

A Pivot prices on two dimensions at once — rows on one field, columns on another. This is how you build a weight × zone rate card, or any grid-style pricing, inside one rule.

- Pick a row field and a column field. For each, choose a match style: **Equals** for discrete values (a carrier name, a zone number), or **Between** for numeric ranges (weight tiers like 0–1 lb, 1–5 lb).
- Paste your whole grid. Copy your numbers from a spreadsheet and paste the entire matrix in at once.
- Empty cells are skipped and cleaned out on save, just like sheets — only cells with values become pricing.

### Which Tool for the Job?

| Use… | When… |
|------|-------|
| **A branch** | You only have a handful of variations, or you're matching on multiple conditions at once (e.g., length AND width AND height for a box size). |
| **A Sheet** | One field with many values — a rate per carrier, per customer, per package type. Populate, fill in, save. |
| **A Pivot** | Two dimensions in one rule — such as weight × zone rate cards. Use Between for numeric ranges like weight tiers, Equals for discrete values like zones. |
| **Duplicate the rule** | A customer needs their own tiered rate or linked fee template. Tiers live at the rule level, so tiered customers always get their own copy of the rule. |

{% hint style="info" %}
Branches (including the ones a sheet creates) hold a single flat fee or markup each. Tiered pricing and linked fee templates are set at the **rule level**, not inside a branch — so any customer on a tiered rate needs their own duplicated rule.
{% endhint %}

## Two Ways to Tier

Tiered rules offer two calculation methods. Pick the one that matches the rate agreement — they produce different totals.

| Method | What it does |
|--------|--------------|
| **Volume Rate** | Every unit is charged at the single tier the total falls into. Example: 25 items, and 25 lands in the top tier — all 25 units bill at that tier's rate. |
| **Graduated Rate** | Each block is charged at its own rate as volume climbs through the tiers — like tax brackets. |

## Customer-Specific Rates: Duplicate, Branch, or Sheet?

To give a customer their own rate, you have three options:

| Method | Best for | How |
|--------|----------|-----|
| **Duplicate the rule** *(recommended default)* | Any rule type — flat, tiered, rate sheets, linked fees. Works in every case. Keep one customer per rule. | Click the 3 dots next to the rule on the Rules page, choose Duplicate, adjust the rate and customer. |
| **Branch by customer** | A few customers in one rule, each with a single flat fee or markup — and the rule isn't already branching on something else. | Add one branch per customer, each scoped to one customer with one flat amount. |
| **Sheet by customer** | Many customers, each with a single flat fee or markup. The fast path. | Add a Sheet with Field = Customer, click Populate, enter a rate per customer, save. Empty rows drop away automatically. |

{% hint style="warning" %}
**Rule of thumb:** Because branches (and sheet rows) can't hold tiered pricing, any customer on a tiered rate needs their own duplicated rule. When in doubt, duplicate — it works for every rule type and takes under a minute.
{% endhint %}

---

## Rule 1 · Standard Unit Pick Fee — Pick & Pack

A fixed dollar amount charged for each unit pulled from the shelf. The most common pick fee structure in 3PL operations — simple, predictable, and easy to explain to any customer.

- **Trigger** — Unit is picked for an order
- **Filter** — Fulfillment Status = Fulfilled
- **Conditions** — None required; applies to all picks by default. Optional: filter by order type.
- **Customer scope** — One customer per rule (duplicate to add a customer). Since this is a single flat fee, you can also branch by customer or use a Sheet by customer to keep everyone in one rule.
- **Action** — Flat fee per unit picked
- **Typical rates** — $0.10–$0.75 per unit (no default — set per customer)

{% hint style="success" %}
**Owlfred prompt:** "Create a pick fee rule labeled [rule name] where each pick is charged at [insert fee] per unit."
{% endhint %}

**Example:** Northwind Supply Co. is charged $0.35 per unit picked. An order with 12 units picked generates a $4.20 pick fee.

## Rule 2 · Pick Fee Tiered by Volume — Pick & Pack

A pick fee where the per-unit rate changes with the number of units in an order — typically rewarding larger orders with a lower per-unit cost. Tiers are based on the number of units (line items) in the order.

- **Trigger** — Unit is picked for an order
- **Filter** — Fulfillment Status = Fulfilled
- **Tier by** — Units (line items) per order
- **Tiering method** — Volume Rate or Graduated Rate (see "Two Ways to Tier" above)
- **Customer scope** — One customer per rule (duplicate per customer). Tiered rules can't be branched or sheeted by customer, so each customer on a tiered rate needs their own copy.
- **Action** — Flat fee per unit at the applicable tier rate
- **Typical rates** — Example: $0.50 for 1–5 units, $0.40 for 6–10, $0.30 for 11+

{% hint style="success" %}
**Owlfred prompt:** "Create a volume tiered pick fee called [rule name]. This should apply to [filter condition]. Here are my rates: Units per order (1-5) $0.50, Units per order (6-10) $0.40, Units per order (11+) $0.30."
{% endhint %}

{% hint style="info" %}
**Tip:** Paste your rate table directly from a spreadsheet. Owlfred reads both columns at once, or each column pasted separately — either format works.
{% endhint %}

**Example (Volume Rate):** Brightline Goods bills a tiered pick fee by units per order: $0.50/unit for 1–5, $0.40/unit for 6–10, $0.30/unit for 11+. An order of 12 units falls in the top tier, so all 12 units bill at $0.30 = $3.60.

## Rule 3 · Order Processing Fee — Orders

A flat fee charged per fulfilled order, regardless of unit count. Can also be structured as a tiered rate based on order or shipment volume. Commonly used alongside a per-item pick fee.

- **Trigger** — Order is fulfilled
- **Filter** — Fulfillment Status = Fulfilled
- **Conditions** — Optional: filter by order type (DTC, wholesale, B2B) or sales channel
- **Tiered option** — Tier By = Number of shipments, using Graduated Rate
- **Customer scope** — Flat version: duplicate per customer, branch, or Sheet by customer. Tiered version: duplicate per customer (tiered rates can't be branched).
- **Action** — Flat fee per order, or tiered rate based on volume
- **Typical rates** — $0.25–$2.00 per order (no default)

{% hint style="info" %}
Owlfred may label this "Fee" rather than "Order Processing" — there is no functional difference.
{% endhint %}

{% hint style="success" %}
**Owlfred prompt (flat):** "Create an order processing fee that applies a [insert fee] fee to each order that is fulfilled."

**Owlfred prompt (tiered):** "Create a tiered order processing fee. Here are my rates: Weekly Base Order Fee (1-1000) $1.60, Weekly Base Order Fee (1001-2000) $1.50, Weekly Base Order Fee (2001+) $1.40."
{% endhint %}

**Example:** Acme Apparel pays a flat $1.75 order processing fee on every fulfilled order. Verve Wellness instead pays a graduated tiered rate by shipment volume: $1.60/order for the first 1,000 shipments, $1.50 for 1,001–2,000, and $1.40 for 2,001+.

## Rule 4 · Carrier Markup (Flat Dollar or Percentage) — Carrier

The most universal billing rule in 3PL operations. Every shipment gets marked up before the brand is charged — either a percentage of the carrier's base rate or a fixed dollar amount per shipment. Most 3PLs run a blanket markup plus customer-specific overrides.

- **Trigger** — Shipment is rated and carrier cost is known
- **Filter** — Cost basis > 0
- **Per-carrier rates** — Use a Sheet with Field = Carrier. Click Populate to list every carrier on your account, enter a markup per carrier, and save — rows you leave empty are deleted automatically, so only the carriers you priced get a rule.
- **Branching by service** — Because rules branch one level deep, carrier and service level can't both be branch dimensions in the same rule. To also differentiate by service, duplicate the rule per service.
- **Customer scope** — All Customers for a universal blanket markup, Some Customers for a group rate. For individual rates: duplicate per customer, or use a branch / Sheet by customer (flat markups only).
- **Action (%)** — Percentage applied to the carrier base rate (most common)
- **Action (flat $)** — Fixed dollar amount per shipment
- **Typical rates** — Varies by carrier, weight class, and customer agreement

{% hint style="warning" %}
**Important:** Always remove a customer from a blanket markup rule once a customer-specific rule is in place for them — otherwise both rules apply to the same shipment, and remember that markups add together. If you build carrier branches manually, configure one carrier at a time; selecting multiple carriers together can make service names display without their carrier label.
{% endhint %}

{% hint style="success" %}
**Owlfred prompt:** "Create a carrier markup rule that charges a [insert percentage] markup anytime the cost basis is greater than 0."
{% endhint %}

**Example:** A blanket rule adds a 12% markup to every shipment's carrier cost. Acme Apparel has its own rule at 8%, reflecting a negotiated rate — and is removed from the blanket rule so only the 8% applies.

## Rule 5 · Third-Party Freight Handling Fee — Carrier

A charge that applies when a brand ships on its own carrier account. Your warehouse is still processing, packing, and handing off the shipment — this compensates for that labor when no carrier margin is being earned.

- **Trigger** — Shipment uses a third-party carrier account or customer-supplied label
- **Filter** — Third-party freight = true
- **Customer scope** — All Customers for a universal rate. Duplicate for one customer or a group if rates differ.
- **Action** — Markup applied when third-party freight is true (can also be configured as a flat fee per shipment)
- **Typical rates** — $1.50–$10.00 per shipment, or a set percentage (no default)

{% hint style="success" %}
**Owlfred prompt:** "Create a third-party freight rule that applies a [insert rate] markup when third-party freight is true [insert any additional conditions]."
{% endhint %}

**Example:** Northwind Supply Co. ships on its own UPS account. Every shipment on that account triggers a 15% third-party freight markup.

## Rule 6 · Carrier Rate Sheet (Weight × Zone) — Carrier

A custom rate card where you build your own pricing matrix — weight on one axis, destination zone on the other. The brand pays according to this agreed rate card, independent of what the carrier actually charges. Used when a negotiated rate schedule has been set at the account level.

- **Trigger** — Shipment is rated (weight and destination zone are known)
- **Filter** — Optional: filter to a specific carrier or service level
- **Configuration** — Build it as a Pivot: weight ranges as rows (Match style = Between), zones as columns (Match style = Equals). Then copy your rate table from your spreadsheet and paste the whole grid in at once — no retyping cell by cell. Empty cells are skipped and cleaned out on save.
- **Fallback rate** — Set a flat rate for any shipment weight or zone not found in the matrix (e.g., $3.00)
- **Customer scope** — One customer per rule — each customer typically has their own negotiated rate card. Duplicate per customer.
- **Typical rates** — Varies by customer and agreed rate card (no default)

{% hint style="warning" %}
**Important:** Always set a fallback rate. Without one, shipments that fall outside your matrix will not be billed. Configure one carrier at a time when building the rate sheet.
{% endhint %}

**Example:** Brightline Goods has a custom rate card: a 3 lb package to Zone 4 bills at $7.25, and a 3 lb package to Zone 8 bills at $9.50. Any shipment outside the matrix falls to a $3.00 fallback rate.

## Rule 7 · Inbound Receiving Fee — Receiving

A fee charged when inventory arrives at the warehouse and is received into the WMS — compensating the 3PL for unloading, counting, and entering product. Can be charged per unit, per carton, or per pallet, depending on how your WMS tracks inbound receipts.

- **Trigger** — Inventory receipt is created in the WMS
- **Filter** — Optional: filter by warehouse
- **Branches** — Branch by warehouse or by package type; each branch can match on multiple conditions. To vary fees across both dimensions, duplicate the rule per warehouse and branch by package type inside each copy.
- **Customer scope** — One customer per rule — duplicate per customer for customer-specific rates.
- **Action** — Flat fee per unit, carton, or pallet received
- **Typical rates** — $0.10–$0.50 per unit | $1.00–$5.00 per carton | $10–$30 per pallet

{% hint style="warning" %}
**Important:** Before configuring, confirm whether your WMS tracks receiving at the unit, carton, or pallet level — this determines which calculation method to select. Check with your implementation contact if you're unsure.
{% endhint %}

**Example:** Acme Apparel is charged $0.20 per unit received at its East warehouse. A shipment of 500 units generates a $100 receiving fee.

## Rule 8 · Returns Processing Fee — Returns

A flat fee charged per return unit received and processed. Covers the cost of inspecting, sorting, and determining final disposition of returned goods — whether restocked, quarantined, or disposed of.

- **Trigger** — Return is received and processed in the WMS
- **Filter** — Is return = true
- **Conditions** — Optional: branch by disposition type (restock vs. destroy vs. quarantine) if fees differ by outcome
- **Customer scope** — One customer per rule — duplicate per customer, or branch / Sheet by customer since this is a single flat fee.
- **Action** — Flat fee per return unit processed
- **Typical rates** — $2.00–$8.00 per return unit (no default)

{% hint style="success" %}
**Owlfred prompt:** "Create a rule that applies a [insert fee] fee per [item/order] when return is true."
{% endhint %}

**Example:** Verve Wellness pays $3.00 per unit on any return. A return of 4 units bills $12.00.

## Rule 9 · Packaging Materials Fee — Packaging

A fee for the physical packaging materials used to fulfill an order, charged per package type (box size, poly bag, mailer, etc.). Each package type gets its own rate, and a fallback catches anything unmatched.

- **Trigger** — Order is packed and label is generated
- **Filter** — None required at top level
- **Branches** — One branch per package type, each defined by its dimensions (e.g., length = 5 AND width = 5 AND height = 5). Because each box is matched on multiple conditions at once, use classic branches here rather than a sheet. Always add a default/fallback branch for any type not explicitly matched.
- **Fallback rate** — Flat catch-all for unmatched package types (e.g., $1.00 per package)
- **Customer scope** — All Customers if the margin is universal. Duplicate per customer for exceptions.
- **Action** — Flat fee per package, matched to the branch for that package type
- **Typical rates** — Varies by material cost. Many clients use a supplies-and-packaging margin.

{% hint style="success" %}
**Owlfred prompt:** "Create a materials rule for [packaging material/type]. Here are my dimensions: 5 x 5 x 5, 10 x 4 x 4, [add more as needed]. And the associated fees: $2.49, $1.89, [add more as needed]."
{% endhint %}

{% hint style="info" %}
**Tip:** Dimensions and fees can be listed together in two columns or separately — Owlfred reads both formats. When branches are defined by multiple dimensions, confirm each branch name maps to the intended fee.
{% endhint %}

{% hint style="warning" %}
**Important:** Box mapping must be confirmed in your WMS before setting this rule up. If your WMS doesn't reliably capture box type per order, the fallback rate will apply to most shipments — verify with your implementation contact before activating.
{% endhint %}

**Example:** A 5x5x5 box bills at $2.49, a 10x4x4 box at $1.89, and anything else falls to a $1.00 fallback rate.

## Rule 10 · Monthly Recurring Fee — Account

A fixed fee charged every billing period, not tied to any order, shipment, or inventory event. This is how 3PLs bill for platform access, technology, account management, or any standing service fee agreed at onboarding. The fee name is fully customizable.

- **Trigger** — Billing period opens
- **Filter** — None (applies at the account level)
- **Customer scope** — One customer per rule — each customer has their own amount and fee name. Duplicate per customer.
- **Fee name** — User-defined. Examples: Technology Fee, Platform Fee, Monthly Service Fee, Account Fee
- **Billing period** — Monthly, weekly, or per billing cycle — set when configuring the rule
- **Action** — Fixed dollar amount per billing period
- **Typical rates** — $50–$500 per month (no default)

{% hint style="success" %}
**Owlfred prompt:** "Create a monthly rule called [rule name] that charges [insert fee] per month."
{% endhint %}

**Example:** Northwind Supply Co. pays a $150/month Platform Fee, billed automatically at the start of each billing period regardless of activity.

---

## Best Practices Summary

- **When in doubt, duplicate.** Duplicate Rule, change the rate and customer — under a minute, and it works for every rule type including tiered rates.
- **Sheets for one dimension, Pivots for two.** A rate per carrier or per customer? Sheet + Populate. Weight × zone or carrier × service? Pivot. Empty rows and cells clean themselves up on save.
- **Branch or sheet by customer only for single flat values.** Tiered pricing and linked fee templates live at the rule level, so tiered customers always get their own duplicated rule.
- **Set a fallback rate.** For rate sheets and packaging rules, unmatched records need somewhere to land or they won't be billed.
- **Set your account default markup.** It's the safety net that keeps any shipment from billing at raw carrier cost when no markup rule matches.
- **Carrier rules: keep blanket and specific rules apart.** Remove a customer from a blanket markup the moment their customer-specific rule goes live — markups add together.
- **Owlfred reads rate tables.** Paste directly from your spreadsheet — into Owlfred, into a Sheet, or into a Pivot. You don't need to retype every line.
- **Confirm your WMS fields first.** For receiving and packaging rules, verify your WMS reliably captures the required data field before activating the rule.

## Common Questions

**Can more than one rule apply to the same shipment?** Yes — that's the intended design. Markups sum, fees stack as separate line items, and discounts apply based on their stackability.

**How do I make a charge apply to only some customers?** Set the rule's customer scope to an include or exclude list.

**How do I make one rule take precedence over another?** Give it a lower priority number. Lower numbers are evaluated first and take precedence where order matters — like choosing which non-stackable discount applies.

**Where do I see which rules were applied to a charge?** Every bill line item records the matching rules and their contributions. The internal bill export also lists the rule names applied to each charge.

**I changed a rule — why didn't my bill update?** Rules apply at bill generation. Regenerate the bill (or all bills in the period) to apply the change. Bills that have already been sent can't be regenerated.

**Do I have to rebuild my exact legacy fee structure?** We recommend starting from these 10 standard structures and layering custom rules on top, rather than recreating a complex legacy spreadsheet exactly. Standard structures are easier to audit and far less error-prone.
