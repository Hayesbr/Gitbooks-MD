# WMS Integrations

A WMS (Warehouse Management System) integration connects Diversifi to the system your 3PL uses to manage orders, shipments, inventory, customers, and warehouses. This data is the foundation of everything in billing — without it, the platform cannot reconcile invoices or apply billing rules.

## What Data Syncs

When a WMS integration is active, Diversifi pulls the following data into the platform:

- **Orders** — order ID, customer, warehouse, line items, parcel count
- **Shipments** — tracking numbers, carrier, service, weight, dimensions, destination ZIP, origin ZIP, quoted cost
- **Customers** — customer name, ID, billing configuration
- **Warehouses** — warehouse name, address, ZIP code
- **Products** — SKU, weight, dimensions (where available)

Diversifi uses the [Data Mapper](data-mapper.md) to transform raw WMS data into a consistent internal format. Each WMS system formats its data differently — the Data Mapper normalizes it so the platform can work with it reliably.

## Supported WMS Providers

| Provider | Notes |
|----------|-------|
| **Extensiv (3PL Central)** | Full integration — orders, shipments, customers, products, warehouses. Extensiv adds markups to quoted amounts in their API, which can affect reconciliation accuracy. See [Carrier Reconciliation](../billing/carrier-reconciliation.md) for the recommended approach. |
| **ShipHero** | Full integration. Voided labels are filtered automatically at the integration level, so voided ShipHero labels are excluded from shipment data. |
| **ShipStation** | Full integration — orders and shipments. |
| **Sandbox** | A test environment integration used for development and QA. Not for production use. |

## How Syncing Works

- **Initial sync** — When a WMS integration is first connected, a full historical pull runs to populate your data.
- **Ongoing syncs** — Subsequent syncs pull only new or updated records since the last sync.
- **Auto-scheduling** — Syncs can be configured to run automatically on a schedule so data stays current without manual intervention. Strongly recommended for active billing accounts.
- **Manual sync** — You can trigger a manual sync at any time from the Integrations page.

{% hint style="warning" %}
**Auto-scheduling is strongly recommended.** Without it, WMS data only updates when someone manually triggers a sync. If syncs aren't running, billing reconciliation will be working against stale shipment data. Enable auto-scheduling for every active WMS integration.
{% endhint %}

## Setting Up a WMS Integration

1. Navigate to Integrations in the left navigation
2. Click Add Integration and select your WMS provider
3. Enter your WMS API credentials — these are provided by your WMS vendor
4. Run an initial sync to pull in your historical data
5. Enable auto-scheduling to keep data current going forward
6. Verify the sync completed successfully by checking the integration status and reviewing a sample of orders and shipments in the platform

## Troubleshooting

| Issue | What to check |
|-------|---------------|
| **Sync not running** | Check that auto-scheduling is enabled. If it is, check the integration status for error messages — a failed sync shows the error reason in the status panel. |
| **Missing shipments** | Some WMS providers require specific permissions on the API key. Confirm with your WMS vendor that the credentials have read access to orders and shipments. |
| **Extensiv markup discrepancy** | Extensiv adds markups to quoted amounts in their API, so the quoted cost Diversifi receives may be higher than the actual carrier cost. See [Carrier Reconciliation](../billing/carrier-reconciliation.md) for the workaround. |
| **Voided labels appearing** | ShipHero voided labels are filtered automatically. If you are seeing voided labels from another WMS, contact support. |
