# Warehouses

Setting up your warehouses correctly before running bids ensures that every bid uses the right rates for the right location automatically.

## What Warehouses Do in BidBoost

When a sales rep runs a bid, the warehouse they select determines:

- **Which rate sets are available** — only rate sets assigned to that warehouse appear as carrier options in the bid
- **The origin ZIP code** — used to calculate zones for every shipment in the bid
- **Which regional carriers apply** — regional carriers like UniUni, OnTrac, and LSO only service certain geographic areas, and the warehouse location determines whether they are viable for a given bid

Without a warehouse configured, the bid flow cannot accurately calculate zones or determine which carriers are available for that location.

## The Warehouses Page

Go to Data → Warehouses to view and manage all warehouses on your account. Each warehouse shows:

- **Name** — the warehouse name as it appears in the bid flow
- **Code** — an optional identifier used to match the warehouse to your WMS or external systems
- **Contact, Email, Phone** — contact details if configured
- **Status** — Active or Inactive; only active warehouses appear in the bid flow
- **Source** — how the warehouse was created (see Warehouse Sources below)

**Searching and filtering** — Use the search bar to find a warehouse by name. Use the Filters button to filter by Data Source (Manual, Integration, or API) or by Sync Override status to find warehouses where manual edits have been made on top of WMS data.

## Warehouse Sources

Every warehouse has a source that indicates how it was created:

- **Integration** — synced automatically from your connected WMS (most warehouses will show this source)
- **Manual** — created directly in Diversifi without a WMS sync
- **API** — created via the Diversifi API

The source determines what you can edit. On an Integration or API warehouse, the WMS ID field is locked — this maintains the connection between Diversifi and your WMS. All other fields can be edited freely.

## Adding a Warehouse

Click + Add Warehouse in the top right corner of the warehouses page and fill in the following:

- **Warehouse name** — a clear descriptive name, for example "Indiana Hub" or "West Coast - Los Angeles." This is what sales reps see when selecting a warehouse in a bid.
- **Warehouse code** — an optional code used to identify the warehouse in external systems. If synced from your WMS, this is populated automatically.
- **Primary address** — the full address including street, city, state, country, and ZIP code. The ZIP code is used to calculate shipping zones for every shipment in a bid, so make sure it's accurate.
- **Active toggle** — new warehouses are active by default. Inactive warehouses do not appear in the bid flow.
- **Advanced options** — expand this section for contact details, external system IDs, dispatch and return addresses, and custom fields. Most users will not need these during initial setup.

Click Save Changes when done.

## Editing a Warehouse

Go to Data → Warehouses, find the warehouse, click the three-dot menu on the right of that row, and select Edit. Update any fields as needed and click Save Changes. On warehouses with a source of Integration or API, the WMS ID field cannot be edited; all other fields can. Changes take effect immediately on any new bids created after the update — existing bids are not affected.

## Overriding and Resetting Warehouse Data

When you edit a warehouse that was synced from your WMS — for example updating the address or name — Diversifi marks that warehouse with an **Override** badge, indicating the warehouse data in Diversifi now differs from your WMS.

**Finding overridden warehouses** — Use Filters → Sync Override → Overridden to see all warehouses with manual edits on top of WMS data.

**Reset to Datasource** — To revert your edits and restore the original WMS data, click Reset to Datasource in the top right corner of the warehouses page. Important things to know:

- It does not affect injection points — injection point configuration is always maintained separately
- Editing injection points does not mark the warehouse as overridden
- Reset to Datasource will not work if the warehouse does not have a valid WMS ID, or if that WMS ID no longer exists in your WMS

## Assigning Rate Sets to a Warehouse

Once your warehouse is created, assign which rate sets apply to it. This controls which carriers and services appear as options when a sales rep selects that warehouse in a bid.

- **From the warehouse** — Go to Data → Warehouses, select the warehouse, and assign the relevant rate sets from the configuration panel.
- **From the cost rates screen** — Go to Carriers → Cost Rates, find the rate set, click the three-dot menu, select Edit, then select which warehouses it applies to.

When a sales rep selects a warehouse during bid creation, only the rate sets assigned to that warehouse appear as carrier options. If no rate sets are assigned, all rate sets on the account are available — the assignment acts as a filter, not a hard restriction. This matters most for accounts with multiple warehouses in different locations: a California FedEx agreement should only appear when the California warehouse is selected, not the Indiana warehouse.

## Injection Points

An injection point is the location where a 3PL drops off shipments for a regional carrier rather than having the carrier pick up from the warehouse directly. Regional carriers typically only operate within specific geographic zones and require shipments to be brought to one of their entry facilities.

**Why injection points matter for bids** — The injection point ZIP code (not the warehouse ZIP code) determines whether a regional carrier can service a given shipment and what the shipping cost will be. If the injection point is not configured correctly, the bid will use the wrong origin for zone calculation on regional carriers, producing inaccurate rates.

**How to set up an injection point** — When adding or editing a warehouse, enter the injection point ZIP code for each regional carrier that requires one. If a carrier picks up directly from your warehouse, you do not need an injection point for that carrier.

{% hint style="info" %}
Editing injection points does not mark the warehouse as overridden and will not be affected by a Reset to Datasource. Injection point configuration is always preserved independently.
{% endhint %}

Common carriers that require injection points: UniUni, OnTrac, LSO, LaserShip / LaserShip Express, Veho, and DoorDash Drive.

## Managing Multiple Warehouses

If your 3PL operates out of multiple locations, you can add as many warehouses as needed. Each warehouse is independent with its own origin ZIP code, injection points, and assigned rate sets. Best practices:

- Give each warehouse a clear name that identifies the location — "FedEx Indiana - Direct" is better than "Warehouse 2"
- Assign only the rate sets relevant for each location — a West Coast DHL agreement should not appear when running a bid out of your Indiana hub
- If you have the same carrier at multiple warehouses but with different rates, create separate rate sets with nicknames that identify the location (e.g. "FedEx Ground - CA" and "FedEx Ground - IN") and assign each to the correct warehouse

## Common Questions

**What happens if I run a bid without selecting a warehouse?** The platform uses your account's default origin ZIP code if one is configured. If no default is set, zone calculations may not be accurate. We recommend always selecting a warehouse when running a bid.

**Can I assign the same rate set to multiple warehouses?** Yes — if the same carrier rates apply across multiple locations, you can assign that rate set to all relevant warehouses. This is common for national carriers like FedEx and UPS where your rates are the same regardless of origin.

**Why is a carrier not showing up when I select a warehouse?** The carrier's rate set is likely not assigned to that warehouse. Go to Carriers → Cost Rates, find the rate set, click Edit, and add the warehouse to its assignment list.

**Why are my zone calculations off on a regional carrier bid?** Check that the injection point ZIP code is entered correctly for that carrier. If it's missing or incorrect, the platform falls back to the warehouse ZIP code, which produces inaccurate results for regional carriers.

**Can I have different injection points for different carriers at the same warehouse?** Yes — each carrier can have its own injection point. This is common when you use multiple regional carriers with different drop-off facilities.

**What does the Override badge mean?** It means the warehouse data in Diversifi has been manually edited and no longer matches your WMS. You can reset it to the original WMS data at any time using Reset to Datasource.

**Will Reset to Datasource remove my injection points?** No — injection points are always preserved and are not affected by a reset.
