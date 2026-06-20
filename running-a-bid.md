# Running a Bid

Once your cost rates are loaded you are ready to run your first bid. This walkthrough covers the full process from start to export. Most bids take under 10 minutes to complete.

## Before You Start

Make sure you have completed the following before running a bid:

- Cost rates loaded for the carriers you want to include
- Carrier configurations set up with DIM factor, fuel, and surcharge settings
- Warehouses added with rate sets assigned and carrier injection points defined

If you haven't done this yet, go to [Cost Rates](cost-rates.md) first.

## Step 1 — Create a New Bid

Go to Sales → Bid Center and click New Bid. You'll be asked to name your bid and select a prospect.

**Selecting a prospect** — Start typing the prospect's company name. If they already exist in the system, select them from the dropdown. If they are new, click Add to create a new prospect record.

**Annual shipping spend** — Select the prospect's estimated annual shipping spend from the dropdown. This is important — it determines which tier of market rate data is used for comparison. A prospect spending $5M annually has more negotiating power than one spending $50K, and the market rates reflect that difference.

## Step 2 — Choose Your Bid Type

Select the bid type based on what data you have from the prospect:

- **PLD — Shipment File** — Upload the prospect's historical shipment file: a spreadsheet of their actual shipments including weight, dimensions, destination ZIP code, and carrier used. Diversifi will rate every shipment in the file against your carrier costs. Accepted file format: Excel (.xlsx).
- **SKU** — Enter the prospect's product SKUs with dimensions and weights. Diversifi will rate each SKU across your selected carriers and zones.
- **No Data** — No prospect data required. Diversifi generates a rate card based on a standard 7 lb package in zone 4 — the most common weight and zone profile in aggregated market data.

## Step 3 — Select Carriers and Services

Choose which carriers and services you want to include in this bid. Only carriers with cost rates loaded in your account will appear here. For each carrier you can select or deselect individual services — for example, you might include FedEx Ground and FedEx Home Delivery but exclude FedEx Express.

{% hint style="info" %}
Whatever you select here is exactly what will appear on the markups screen and in your exports. Only selected carriers and services will be used in the bid — nothing extra will be included.
{% endhint %}

If you have assigned rate sets to a warehouse and selected that warehouse, only the rate sets assigned to that warehouse will be available to select.

## Step 4 — Apply Your Markup

The markups screen is where you set how much margin you want to make on top of your cost rates. Once your file is processed, your shipments are grouped by speed tier so you can see exactly where every package in the file went and make informed markup decisions.

Your shipments are organized into groups based on transit time:

- **Next Day** — shipments where a next day service is the winning option
- **2–3 Day** — shipments where a 2 to 3 day ground or express service wins
- **4–5+ Day** — shipments where a slower ground service wins
- **Unrated** — shipments where Diversifi could not determine a speed tier based on the data available. These are shown at the bottom so you can see them, but they do not affect the rated results above.

Each speed tier group shows the average cost per package, and a badge identifies the winning carrier and service — the one with the lowest average cost per package after all markups are applied. As you increase the markup on a carrier or service, the average cost per package updates in real time, so you can find the markup level where your margin is maximized without losing the win to a competitor carrier.

For full detail on the markups screen, see [Markups & Surcharges](markups-and-surcharges.md).

**Adjusting markups** — Use the slider for each carrier and service to adjust the markup individually. To apply a blanket markup across all carriers or all services at once, use the Quick Actions panel.

**Fuel and surcharges** — Toggle on any additional fees you want to include in the prospect's rates: fuel surcharge, residential surcharge, and additional handling / oversize.

## Step 5 — Review and Export

Once you are happy with your markups, review the KPI cards at the top of the screen:

- **Total proposed cost** — what the prospect would pay in total using your rates
- **Estimated savings** — how much they would save compared to their current rates
- **Savings percentage** — the percentage reduction from their current spend
- **Average cost per shipment** — the average proposed rate per package

If the numbers look right, click Export and choose your export type — Net Rate, Blended Rate, or Shipment File. (Shipment File is only available on PLD bids.) See [Exports](exports.md) for full detail. Your export file will be named: ProspectName_NickName_ExportType.

## Tips for a Strong Bid

- **Use PLD when you can.** A shipment file bid is always more compelling than a No Data bid because it uses the prospect's real data. Push to get a shipment file whenever possible.
- **Start with a conservative markup.** It is easier to come down on price than to go up. Start with a markup that gives you healthy margin and adjust if the prospect pushes back.
- **Run the bid with 0% markup first.** Before applying your markup, run a quick export at 0% to verify your cost rates are loading correctly. The export should match your cost rate sheet exactly. If it doesn't, check your carrier configuration and rate set assignments.

## Common Questions

**Why is a carrier not showing up in my bid?** The carrier either doesn't have cost rates loaded, or the rate set isn't assigned to the selected warehouse. Go to Carriers → Cost Rates and confirm the rates are loaded and assigned correctly.

**Why are there services showing up that I didn't select?** Make sure you are deselecting services you don't want before proceeding past the carrier selection screen. Only selected services should appear on the markups screen and in exports.

**Why does my export show different rates than my cost rates?** The most common causes are a surcharge toggle being on or a markup being applied. Run the bid again at 0% markup with all surcharge toggles off and compare to your cost rate sheet.

**Can I save a bid and come back to it?** Yes — bids are saved automatically. Go to Sales → Bid Center to find all your saved bids.

**Can I share a bid with a colleague?** Yes — from the bid you can share it with other users on your account.
