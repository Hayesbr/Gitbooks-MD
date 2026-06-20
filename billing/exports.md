# Billing Exports

Every bill in Diversifi can be exported once it has been reviewed and approved. Billing exports are how you share billing information with your customers and how your internal team keeps records of what was billed, what the actual costs were, and what margin was generated. Diversifi provides two distinct export types for every bill — one for internal use and one that is safe to send directly to your customer.

## Two Export Types

**Internal export** — Contains the full detail behind every charge on the bill: rule names, markup amounts, quoted vs. actual costs, margin per shipment, and all carrier cost data. This version is for your billing team's records and should never be shared with a customer — it contains your cost structure and margin information.

**Customer-facing export** — A clean version that shows charge descriptions and amounts only. No internal cost data, no markup visibility, no rule names, no margin information. This is the version you send directly to your customer. It is formatted to be readable and professional without exposing any of your pricing logic.

Both export types follow the same four-section structure as the bill itself. Each section can be exported individually or all together as part of a full bill export.

## Exporting a Bill

Go to Billing → Customer Billing → Bills, open the approved bill you want to export, and click Export in the top right corner. From the export panel you can:

- **Choose your export type** — Select Internal or Customer-facing depending on who will receive the file.
- **Choose which sections to include** — Select all four sections for a complete bill export, or select individual sections if you only need a specific part. For example, if a customer only wants to see their parcel charges for the period, you can export just that section.
- **Choose your file format** — All exports are available as Excel (.xlsx), formatted and ready to send without additional editing.
- **Name your file** — Export files are named automatically using the customer name, billing period, and export type — for example, `Acme Brands — May 16-31 — Customer Bill.xlsx`. You can rename the file before downloading if needed.

## Bulk Export

To export bills for multiple customers at once, go to Billing → Customer Billing → Periods, open the period you want to export, and select the bills you want to include. Click Bulk export and choose your export type. Diversifi packages all selected bills into a zip folder, with each file named after the customer so they are easy to identify and distribute. This is useful at the end of a billing cycle when you need to send exports to all customers at once.

## Sending to QuickBooks

In addition to file exports, Diversifi can push approved bills directly to QuickBooks. From an approved bill, click Send to QuickBooks and the bill is transmitted automatically; the bill status then changes to Sent and the bill is locked. Diversifi maps the bill sections to the corresponding line items in QuickBooks so the invoice matches your bill structure. Contact your Diversifi account manager to configure your QuickBooks integration if it is not yet connected.

## What Each Export Contains

**Internal export — parcel charges:** tracking number, order number, carrier and service, ship date, destination ZIP code, quoted amount (from WMS), actual carrier cost, variance, markup applied, pick fee, pack fee, packaging fee, handling fee, DAS / RAS surcharges if applicable, and total charge.

**Customer-facing export — parcel charges:** tracking number, order number, carrier and service, ship date, destination ZIP code, shipping charge, pick fee, pack fee, packaging fee, handling fee, and total charge.

**Internal export — order charges:** order number, ship date, number of parcels in order, rule name applied, fee amount, and total charge.

**Customer-facing export — order charges:** order number, ship date, number of parcels in order, fee description, and total charge.

**Both export types — adjustments:** tracking number, original billed amount, actual carrier cost, adjustment amount, and a note explaining the adjustment reason.

**Both export types — other fees:** fee description, amount, date added (and "added by" on the internal export only).

## Common Questions

**Can I customize which columns appear in my export?** Column customization and saved export templates are planned for a future release. Currently the column set is standard across all accounts for each export type.

**Can I export a bill before it is approved?** No — exports are only available on bills with a status of Approved or Sent. Bills still in review cannot be exported.

**Can I re-export a bill after it has been sent?** Yes — sent bills can be re-exported at any time. Re-exporting does not change the bill or its status; it simply downloads a fresh copy of the same approved data.

**What happens if I export the wrong version and send the internal export to a customer?** Contact your Diversifi account manager immediately. There is no way to unsend an email, but your account manager can help you communicate with the customer. Going forward, use the Customer-facing export type for all outbound files — the label on the export panel clearly distinguishes the two.

**Why does my customer-facing export show different totals than my internal export?** The totals should match — both versions bill the customer the same amount. The only difference is what detail is shown. If you see different totals, contact your account manager, as that would indicate a data issue.

**Can I add additional columns to the customer-facing export for a specific customer?** Not currently — column customization per customer is planned for a future release. If a customer has specific column requirements, use the bulk export and reformat the file before sending.
