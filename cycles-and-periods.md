# Cycles and Periods

Cycles and periods are the foundation of how billing is organized in Diversifi. A cycle defines the rules for how a group of customers gets billed. A period is the specific time window within that cycle where bills are generated. Together they give you full control over billing cadence, data source, and customer grouping.

## What Is a Cycle?

A cycle is a billing configuration that applies to a group of customers. It defines:

- What type of activity is being billed — transportation, fulfillment, or both
- What data the billing is based on — carrier invoice or WMS shipments
- Which customers are included
- How often bills are generated

You can have multiple cycles running at the same time. For example, you might have one weekly cycle for transportation billing and a separate monthly cycle for warehousing fees. Customers can be in multiple cycles if they are billed for different activity types on different cadences.

## Creating a Cycle

Go to Billing → Customer Billing → Cycles and click New Billing Cycle.

1. **Name your cycle** — Give it a descriptive name that identifies the customer group or billing type, for example "Weekly Transportation — FedEx Customers" or "Monthly Fulfillment Fees."
2. **Choose the billing type** — Select what activity this cycle will bill for: Transportation only, Fulfillment / warehouse fees only, or Both.
3. **Choose what the billing is based on** — This is one of the most important decisions when setting up a cycle. Select the data source that drives billing:
   - *Carrier invoice — by invoice date (recommended)* — Bills are generated based on when carrier invoices are received. This is the cleanest method because you are billing on confirmed actual carrier data.
   - *Carrier invoice — by ship date* — Bills are generated based on the ship date on the carrier invoice rather than the receipt date. This can pull historical charges into current periods if invoices arrive late. Use only if your customer contracts require ship date billing.
   - *WMS shipments — by ship date* — Bills are generated based on the quoted cost from your WMS rather than the actual carrier invoice. Use this when billing on rate shop estimates rather than reconciled actuals.
4. **Set the cadence** — Choose how often bills are generated within this cycle — weekly, bi-weekly, or monthly. Select the start date and the day of the week or month the cycle repeats on.
5. **Assign customers** — Select which customers belong to this cycle. A customer can only be in one cycle per billing type — a customer cannot be in two transportation cycles simultaneously.

Click Create Cycle to save.

{% hint style="info" %}
Our recommendation is carrier invoice by invoice date for all new customers. It is the industry standard and produces the least confusion and variance.
{% endhint %}

## What Is a Period?

A period is a specific billing window within a cycle. If your cycle runs weekly starting Monday, each week is a separate period. Periods are created automatically when a cycle is set up — you do not need to create them manually. Each period generates bills for all customers in that cycle for activity that falls within that period's date range.

**Viewing periods** — Go to Billing → Customer Billing → Cycles, select a cycle, and click into the Periods tab. You will see all periods for that cycle listed chronologically with their status — open, in review, or closed.

## Editing a Cycle

Go to Billing → Customer Billing → Cycles, find the cycle you want to update, and click Edit. You can update the cycle name, billing type, billing basis, cadence, and customer assignments. Changes take effect on the next period that is generated — existing periods and bills already created are not affected.

**Adding or removing customers from a cycle** — Open the cycle and go to the Customers tab. Add customers from the dropdown; remove them with the remove action next to their name. Customers removed from a cycle will not appear in future periods, but their existing bills are preserved.

## Managing Periods

**Generating bills for a period** — Once a period's date range has closed, Diversifi generates bills automatically for all customers in the cycle. You can also manually trigger bill generation from the period page if you need to run it before the period closes.

**Regenerating bills** — If you update your billing rules after bills have been generated, you can regenerate them to apply the new rules. Go to the period, select the bills you want to regenerate, and click Regenerate. You can regenerate individual bills or all bills in a period at once. Regenerating recalculates all fees using your current rules against the existing data — it does not change the underlying data.

**Period limits** — Each cycle supports up to 10 open periods at a time before bills have been produced. Once bills are generated for existing periods, additional periods can be created. If you need more periods than this limit allows, archive or close existing periods first.

## Cycle Status and Bill Status

**Cycle statuses:**

- **Active** — the cycle is running and generating periods normally
- **Paused** — temporarily stopped; no new periods will be generated until resumed
- **Archived** — closed; historical periods and bills are preserved but no new periods will be generated

**Period statuses:**

- **Open** — within its date range and accepting new data
- **In Review** — closed, and bills are being reviewed before sending
- **Closed** — all bills in the period have been approved and sent

**Bill statuses:**

- **Needs Review** — generated and waiting for your team to review
- **Needs Approval** — all four sections reviewed and ready for final approval
- **Approved** — approved and ready to send
- **Sent** — sent externally and locked

## Common Questions

**Can a customer be in more than one cycle?** Yes — a customer can be in a transportation cycle and a fulfillment cycle simultaneously. They cannot be in two cycles of the same billing type at the same time.

**What happens if I forget to assign a customer to a cycle?** You can add them at any time. They'll be included in the next period that generates after you add them. Historical periods they were not in are not retroactively updated.

**Can I pause billing for a specific customer without removing them from the cycle?** Currently, pausing is done at the cycle level, not the customer level. To pause billing for one customer without affecting others, remove them from the cycle and add them back when billing should resume.

**What happens to existing bills if I archive a cycle?** All existing bills are preserved exactly as they are. Archiving stops future periods from being created but does not affect bills already generated, reviewed, or sent.

**What is the difference between regenerating a bill and creating a new one?** Regenerating recalculates fees on an existing bill using your current rules. It does not change the date range or underlying data. Creating a new bill from scratch is only possible by creating a new period.

**Can I change the billing basis after a cycle has been created?** Yes — you can edit the billing basis at any time. The change applies to the next period generated after the edit. Existing periods use the basis that was in place when they were created.
