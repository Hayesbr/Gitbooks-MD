# Billing Rules

Billing rules are what tell Diversifi how to calculate each fee on every bill. Instead of building charges by hand in a spreadsheet, you define rules once and Diversifi applies them automatically every time a bill is generated.

A rule answers two questions: _when_ should a charge apply, and _what_ is the charge? For example: "When a unit is picked for an order, charge a $0.50 pick fee per unit," or "When an order ships, add a flat $2.00 order processing fee."

{% hint style="info" %}
A WMS integration is required before you can create billing rules. Rules are evaluated against your order and shipment data, so the platform needs at least one active WMS integration connected first. See [WMS Integrations](../integrations/wms-integrations.md).
{% endhint %}

## Anatomy of a Rule

Every rule is built from the same parts:

* **Trigger (event)** — the event that the rule reacts to: a unit being picked, an order shipping, a parcel being delivered, an inbound shipment being received, a return being processed, and so on.
* **Data set** — the type of activity the rule applies to (parcels, orders, returns, receipts, etc.). Which data is available depends on your WMS.
* **Conditions** — an optional set of tests that must be true for the rule to apply, combined with AND/OR logic. For example, "order type is DTC" AND "item count is greater than 3." A rule with no conditions applies to every matching event.
* **Branches** — optional variations within a rule. The most common branch is by carrier or service type, so a single rule can handle different rates across different carriers or services.
* **Action** — what the rule does when it matches. There are three action types (below).
* **Customer scope** — which customers the rule applies to: all customers, an include list, or an exclude list.
* **Priority** — controls the order in which rules are evaluated. A lower number is higher priority.

## The Three Action Types

Every rule applies one of three kinds of charge:

* **Markup** — increases the cost basis (typically the carrier cost) by a percentage, a flat dollar amount, or a multiplier. This is how you build your margin into transportation charges.
* **Fee** — adds a charge such as a pick fee, packaging fee, or handling fee.
* **Discount** — reduces the charge, for example a volume or loyalty discount.

## How Multiple Rules Combine

Diversifi evaluates **all** of your rules against each shipment, and **every matching rule contributes** to the final charge. This lets you layer simple rules into sophisticated pricing instead of writing one giant rule for every scenario. The way matches combine depends on the action type:

*   **Markups are additive.** If three markup rules match the same shipment, their amounts are summed. Percentage markups are applied to the cost basis and added together; flat-amount markups are added directly. (Multipliers are converted to a markup amount and summed, not compounded.)

    _Example:_ a 10% markup + a 5% markup + a $2.00 flat markup on a shipment = (cost basis × 15%) + $2.00.
* **Fees are cumulative.** Each matching fee rule creates its own line item on the bill, so a fuel surcharge, a residential fee, and a handling fee can all apply to the same shipment and each appears separately.
* **Discounts respect stackability.** Each discount can be marked stackable or not. Stackable discounts all apply together; if a non-stackable discount matches, only one non-stackable discount is applied (the highest-priority one).

**Calculation order:** Diversifi first calculates the total markup from all matching markup rules (or the system default if none match), adds it to the cost basis to get a subtotal, then calculates fees (based on the cost basis) and discounts (based on the subtotal) as separate tracked amounts.

Every matching rule and its contribution is recorded on the bill line item, so you always have a full audit trail of why a charge is what it is.

## Priority

Rules are evaluated in priority order, from lowest number to highest (priority 1 is evaluated before priority 100). Priority determines the order fees and discounts are applied and which rule is treated as the primary rule when it matters — for example, when a non-stackable discount has to be chosen. If you don't set a priority, the rule uses a default. Use lower numbers for the rules that should take precedence.

## Customer Scope

Each rule can apply to:

* **All customers** — the default; the rule is evaluated for every customer in the cycle
* **Include list** — only the customers you select
* **Exclude list** — every customer except the ones you select

This lets you keep one standard rule set across your book of business while carving out exceptions for specific customers.

## What Happens When No Rule Matches

If no markup rule matches a shipment, Diversifi applies your account's default markup so the shipment is never billed at raw cost. Set a sensible default markup on your account so there is always a safety net.

## Common Rule Types

These are the standard rule structures most 3PLs configure. They are a starting point — you can add custom rules on top.

| Rule type                              | What it does                                                                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Standard Unit Pick Fee**             | A flat fee per unit picked. Optionally make the first N picks per order free. Branch by customer for different per-unit rates. |
| **Pick Fee Tiered by Volume**          | A pick fee that decreases as monthly volume increases — rewards higher-volume customers with a lower per-pick rate.            |
| **Order Processing Fee**               | A flat fee charged once per order regardless of how many boxes ship. Can be tiered by unit count or order value.               |
| **Carrier Markup**                     | A flat dollar or percentage markup applied on top of carrier cost — your transportation margin.                                |
| **Third-Party Freight Handling Fee**   | A handling fee applied to freight moved through a third party.                                                                 |
| **Carrier Rate Sheet (Weight × Zone)** | Bills transportation off a defined weight-by-zone rate table rather than a simple markup.                                      |
| **Inbound Receiving Fee**              | A fee charged when inbound shipments are received into the warehouse.                                                          |
| **Returns Processing Fee**             | A fee charged when a return is processed.                                                                                      |
| **Packaging Materials Fee**            | A fee for packaging materials used to fulfill an order.                                                                        |
| **Monthly Recurring Fee**              | A fixed recurring charge at the account level, such as a technology or account-management fee.                                 |

{% hint style="info" %}
Some fee types depend on data fields that not every WMS provides. If a rule relies on data your WMS doesn't supply, it can't be evaluated accurately — your account manager will confirm what's available for your integration during onboarding.
{% endhint %}

## Applying Rule Changes to Existing Bills

Rules are applied automatically when a bill is generated. If you change a rule after bills already exist, regenerate the affected bills to apply the update. You can regenerate an individual bill or all bills in a period at once. Regenerating recalculates the fees using your current rules against the same underlying data — it does not change the shipment or invoice data itself, and it cannot be done on a bill that has already been sent. See [Cycles and Periods](cycles-and-periods.md) for how to regenerate.

## Common Questions

**Do I have to rebuild my exact existing fee structure?** Diversifi is built around standard, industry-tested rule patterns. We recommend starting from the standard rule types and layering custom rules on top, rather than recreating a complex legacy spreadsheet exactly. Standard structures are easier to audit and far less error-prone.

**Can more than one rule apply to the same shipment?** Yes — that's the intended design. All matching rules apply: markups sum, fees stack as separate line items, and discounts apply based on their stackability.

**How do I make a charge apply to only some customers?** Set the rule's customer scope to an include or exclude list.

**How do I make sure one rule takes precedence over another?** Give it a lower priority number. Lower numbers are evaluated first and take precedence where order matters.

**Where do I see which rules were applied to a charge?** Every bill line item records the matching rules and their contributions. The internal bill export also lists the rule names applied to each charge.
