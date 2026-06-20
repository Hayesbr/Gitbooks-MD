# Multi-Shipment Logic

When a customer orders multiple products that ship in more than one box, the order becomes a multi-shipment. Managing the cost of multi-shipment orders is one of the most common sources of large variance in carrier reconciliation — not because anything is wrong with the billing, but because different WMS systems record the shipping cost in different ways. Multi-shipment logic is how Diversifi normalizes these costs so your reconciliation numbers are accurate and your bills make sense to your customers.

## The Problem

When a carrier ships multiple boxes under the same order, they generate one combined cost for the entire shipment. How that cost gets recorded in your WMS depends on which WMS you use. The three most common approaches are:

- **Scenario 1 — All costs on the first package** — The WMS assigns the full shipping cost to the lead tracking number (the first box) and records zero for all other boxes in the order. This is the most common approach.
- **Scenario 2 — Total cost duplicated across all packages** — The WMS records the full total cost on every tracking number. If the total was $30 across three boxes, each box shows $30 — making it look like the total cost was $90.
- **Scenario 3 — Only the first tracking number is listed** — The WMS records a single tracking number for the entire shipment regardless of how many boxes went out. The other boxes are not recorded individually.

Each of these creates the same downstream problem: when Diversifi reconciles the quoted WMS cost against the actual carrier invoice — which lists each tracking number individually with its share of the cost — the variance looks enormous. A customer account that is actually running smoothly can look like it has hundreds of dollars of unexplained differences simply because of how the WMS handled the cost allocation.

## How Diversifi Handles It

Diversifi's multi-shipment logic normalizes costs across all packages in a multi-shipment order using a weighted-average approach. When enabled, the system identifies all packages that belong to the same multi-shipment group, calculates the true cost per pound, and redistributes the costs proportionally based on each package's weight.

**Grouping logic** — Packages are grouped into the same multi-shipment group when they share all four of the following:

- Same order number
- Same carrier
- Same service level
- Same ship date

Ship date and carrier are part of the grouping because the same order can sometimes ship in multiple batches on different days or use different carriers for different boxes. Including them ensures each grouping is precise and costs aren't pooled across separate shipments.

**Cost redistribution** — Once a group is identified, the system:

1. Sums the total shipping cost across all packages in the group
2. Sums the total weight across all packages in the group
3. Divides total cost by total weight to get an average cost per pound
4. Multiplies each package's weight by the average cost per pound to get that package's redistributed cost
5. Replaces the original cost on each package with the redistributed amount

The result is that each package carries a proportional share of the true shipping cost based on its weight, rather than an artificially inflated or deflated number from the WMS.

**Visual indicator** — Any package whose cost has been redistributed is marked with an indicator in the billing UI, so your team can see at a glance which line items have been normalized. You can always tell which costs are WMS originals and which have been redistributed.

## Incomplete Data Handling

Multi-shipment logic requires complete weight data for every package in the group before redistribution can occur. If any package in the group is missing a weight value — which typically happens when the WMS has not yet finished updating the package record — the system will not redistribute costs for that group. It waits until all required data is available, then runs the redistribution automatically once the missing weight data arrives.

This prevents partial or inaccurate redistributions from appearing in your billing — it is better to show the original WMS cost temporarily than to redistribute based on incomplete information.

## How to Enable Multi-Shipment Logic

Multi-shipment logic is turned off by default. To enable it:

1. Go to Integrations in the left navigation
2. Select the WMS integration you want to configure
3. Find the **Multi-shipment cost logic** toggle
4. Turn it on

The setting is configured per WMS integration. If you have multiple WMS integrations, you can enable multi-shipment logic on each one independently depending on how that WMS handles multi-shipment cost recording.

## Which WMS Scenario Do I Have?

The easiest way to determine your scenario is to find a multi-shipment order in your WMS and look at how the shipping cost is recorded across the individual tracking numbers:

- If only the first tracking number has a cost and the rest show zero — **Scenario 1**
- If every tracking number shows the same total cost — **Scenario 2**
- If only one tracking number is listed regardless of box count — **Scenario 3**

For Scenario 3, Diversifi's multi-shipment logic handles redistribution where possible. However, because only one tracking number is recorded, some orders may not be fully reconcilable; in those cases, corrections are handled through the Adjustments section of the bill.

**Known WMS behaviors:**

- **Extensiv** — records the full total cost on every tracking number (Scenario 2)
- **ShipHero** — varies by configuration
- **ShipStation** — typically records costs on the lead tracking number (Scenario 1)

Contact your Diversifi account manager if you are unsure how your WMS records multi-shipment costs.

## Common Questions

**Will enabling multi-shipment logic change my existing bills?** No — it applies to data going forward from the point you enable it. Bills that have already been generated and sent are not retroactively changed.

**Why does my reconciliation show large variances even on orders I know are correct?** Large variances on multi-shipment orders are almost always caused by how the WMS records costs across multiple tracking numbers, not an actual billing error. Enabling multi-shipment logic normalizes these costs and significantly reduces the variance on affected orders.

**What if the redistributed costs still don't match the carrier invoice exactly?** Small differences may remain after redistribution due to rounding or carrier surcharges applied at the parcel level. These appear as adjustments in the next billing period through the standard reconciliation process.

**Can I see which orders were affected by multi-shipment logic?** Yes — any package whose cost was redistributed is marked with an indicator in the billing UI. You can identify all affected line items in the bill detail view.

**What happens if a package weight comes in after the bill has already been generated?** If the missing weight data arrives after a bill has been generated, the redistribution applies to the next billing period for that order as an adjustment rather than retroactively changing the closed bill.
