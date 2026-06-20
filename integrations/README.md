# Integrations Overview

Diversifi connects to the external systems your 3PL already uses — your warehouse management system, your carriers, and your billing tools — so that data flows in automatically without manual entry. This section covers how those connections work and what each one does.

## Why Integrations Matter

Diversifi's billing and bids products are only as accurate as the data flowing into them. Integrations are what make that data live and automatic instead of manual and error-prone.

- **Without a WMS integration** — billing rules cannot fire correctly because there is no order and shipment data to evaluate them against
- **Without a carrier integration** — reconciliation must be done manually by uploading invoice files instead of syncing automatically
- **Without accurate data** — bid exports and billing calculations may reflect incomplete or outdated information

## The Types of Integrations

**WMS Integrations** — Connect your warehouse management system (Extensiv, ShipHero, ShipStation, and others) to pull in orders, shipments, customers, warehouses, and products. This data powers billing reconciliation and rules. See [WMS Integrations](wms-integrations.md).

**Carrier Integrations** — Connect your carrier accounts to pull in carrier invoices automatically for reconciliation. Powered by Trackstar. Supported carriers include FedEx, UPS, USPS, DHL, and more. See [Carrier Integrations](carrier-integrations.md).

**API** — Connect Diversifi to your own internal systems or third-party tools via the Diversifi API. Contact your account manager for API documentation and access.

## Integration Status

You can view the status of all configured integrations from the Integrations section in the left navigation. Each integration shows its connection status, last sync time, and any errors that need attention. Auto-scheduling is available for WMS integrations — syncs can be configured to run on a schedule so your data stays current without manual kicks.

{% hint style="info" %}
A WMS integration is required before billing rules can be created. The platform gates rule creation to accounts that have at least one active WMS integration configured.
{% endhint %}
