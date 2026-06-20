# Bill Review

Bill review is the step between a bill being generated and a bill being sent to your customer. Every bill Diversifi generates goes through a structured review process before it can be approved and sent. This ensures that fees are calculating correctly, rules are applying as expected, and nothing unexpected ended up on the bill before it reaches your customer.

## How Bills Are Generated

Bills are generated automatically at the end of each billing period based on the cycle configuration. When a period closes, Diversifi pulls in all shipment data, carrier invoice data, and fulfillment activity for that period, runs your billing rules against it, and produces a bill for each customer in the cycle.

You can also manually trigger bill generation from the periods page if you need to generate a bill before the period closes naturally. Once generated, every bill starts with a status of **Needs Review**.

## The Four Review Sections

Every bill is broken into four sections that correspond to the four types of charges that can appear on a bill. Your team reviews each section independently before the bill can be approved.

- **Parcel charges** — All fees tied to individual shipments at the tracking number level: the quoted amount from the WMS, the actual carrier cost from the invoice, the variance between the two, your markup, pick and pack fees, packaging fees, and handling fees. If a fee applies to a specific box or tracking number, it shows up here.
- **Order charges** — Fees that apply at the order level regardless of how many boxes shipped. The most common example is an order processing fee — a flat fee charged once per order. Tiered order fees based on unit count or order value also appear here.
- **Adjustments** — Late carrier invoices and reconciliation differences. When a carrier invoice arrives after a billing period has closed, or when the actual carrier cost differs from the quoted amount that was already billed, the delta appears here as an adjustment on the next bill. This section is the result of the reconciliation process.
- **Other fees** — Any fee that does not fit at the parcel or order level: storage fees, technology fees, admin fees, monthly minimums, and any ad hoc manual charges or discounts added by your team.

## Reviewing a Bill

Go to Billing → Customer Billing → Bills and select the bill you want to review. Bills with a status of Needs Review are at the top of the queue. The bill opens showing the summary view — total amounts for each of the four sections and the combined bill total. From here you can drill into each section to see the individual line items.

**Reviewing each section** — Click into a section to see all line items. Review the charges, confirm the rules applied correctly, and check for anything unexpected. When you are satisfied with a section, click **Mark as reviewed**. The section status changes from Needs Review to Reviewed.

**Marking all sections at once** — To mark all four sections reviewed in a single action, use the **Mark all as reviewed** button at the top of the bill. This is useful when bills are straightforward and you have already spot-checked the numbers.

**Audit trail** — Every review action is logged. Diversifi records which team member reviewed each section and when. This audit trail is visible on the bill and cannot be edited, providing a clear record of who signed off on what before the bill went out.

## Adding Fees or Discounts

If you need to add a charge or discount that was not captured by your rules, you can do so from the **Other Fees** section. Click into Other Fees and select Add fee or Add discount, then enter the description, amount, and any notes. The fee or discount is added to the bill immediately and included in the bill total. Common uses:

- A storage fee that was not covered by a rule
- A one-time setup or onboarding fee
- A discount agreed with the customer outside of the standard rule set
- A correction for an error on a previous bill

## Regenerating a Bill

If you make changes to your billing rules after a bill has been generated, you can regenerate the bill to apply the updated rules. Go to the bill and click **Regenerate bill** — Diversifi re-runs your current rules against the same underlying shipment and invoice data and produces a new set of charges, replacing the previous version.

You can also regenerate all bills in a period at once from the period page. Regenerating is useful when a rule change should apply to all customers in the cycle for that period.

{% hint style="warning" %}
You can only regenerate a bill that has not yet been sent. Once a bill is sent it is locked and cannot be regenerated. Any corrections to a sent bill appear as adjustments on the next period.
{% endhint %}

## Bill Statuses

- **Needs Review** — the bill has been generated and is waiting for your team to review all four sections
- **Needs Approval** — all four sections have been marked reviewed and the bill is ready for final sign-off before sending
- **Approved** — the bill has been approved and is ready to send to the customer
- **Sent** — the bill has been sent externally and is locked; no further edits are possible

## Approving and Sending a Bill

Once all four sections are reviewed, the bill status moves to Needs Approval. A team member with approval permissions reviews the bill total and clicks Approve. After approval, the status moves to Approved, and from here you can:

- **Export the customer-facing bill** — a clean export showing charge descriptions and amounts with no internal cost or margin data. Safe to send directly to the customer.
- **Export the internal bill** — the full detail version showing rule names, markup amounts, quoted vs. actual costs, and margin. For your team's records only.
- **Send to QuickBooks** — push the approved bill directly to QuickBooks for invoicing.

Once the bill is sent, the status changes to Sent and the bill is locked. If you need to make corrections after sending, they will appear as adjustments on the next billing period.

## Handling Disputes and Corrections

If a customer disputes a charge on a sent bill, do not attempt to edit the sent bill. Instead, handle corrections through the adjustments process on the next billing period. This keeps a clean audit trail and ensures your billing history stays intact. If a dispute is significant and needs to be resolved before the next billing period, contact your Diversifi account manager to discuss options.

## Common Questions

**Can I review bills from my phone or tablet?** Yes — the bill review experience is accessible on any device through the Diversifi web app. The four-section layout works on both desktop and mobile screens.

**What happens if I accidentally mark a section as reviewed?** You can unmark a section as reviewed before the bill is approved. Once the bill is approved and sent, the audit trail is locked and cannot be changed.

**Can two people review the bill at the same time?** Yes — multiple team members can review different sections simultaneously. The audit trail records each reviewer individually so you can see who reviewed what.

**Why does the Adjustments section sometimes have negative amounts?** A negative adjustment means the actual carrier cost came in lower than what was quoted and already billed. The customer was overcharged on the previous bill, and the negative adjustment credits them back on the current one.

**Can I set up a rule to automatically approve bills that are under a certain amount?** Not currently — all bills require manual review and approval before they can be sent. This ensures accuracy and accountability on every bill.

**What is the difference between Needs Approval and Approved?** Needs Approval means all sections have been reviewed but the final approval step has not been completed. Approved means a team member with approval permissions has given final sign-off and the bill is ready to send. This two-step process ensures a second set of eyes on the bill before it goes to the customer.
