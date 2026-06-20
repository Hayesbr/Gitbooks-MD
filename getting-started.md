# Getting Started

Welcome to Diversifi. This guide will walk you through everything you need to get up and running on the platform. Most 3PLs are fully set up within their first week.

## What You'll Need Before You Begin

Before logging in for the first time, make sure you have the following ready:

- Your carrier rate sheets — you'll need these to load your cost rates into the platform
- Your WMS login credentials — to connect your warehouse management system
- Your team's email addresses — to invite the people who will be using the platform

## Step 1 — Set Up Your Account

When you receive your invite email from Diversifi, click the link to create your account. You'll be asked to set your name, password, and timezone.

Once you're in, go to Settings → Account to complete your company profile, including your company name and address.

## Step 2 — Invite Your Team

Go to Settings → Users and invite the team members who will be using the platform. Diversifi has three user roles:

- **Owner** — full access including user management, warehouse setup, integrations, and billing settings
- **Manager** — full access to all platform features
- **Regular** — can run bids, manage billing records, and view reports; cannot manage users or integrations

At least one person on your team should be set to Owner. We recommend having two Owners so there is always a backup administrator.

## Step 3 — Connect Your WMS

Go to Integrations in the left navigation and connect your warehouse management system. Diversifi supports Extensiv, ShipHero, and ShipStation.

Connecting your WMS allows Diversifi to automatically pull in your shipment data, order data, and customer information — which is the foundation for both BidBoost and Billing.

{% hint style="info" %}
If you are setting up carrier integrations as well, do not use both email invoice ingest and a carrier integration for the same carrier at the same time. Use one or the other to avoid duplicate invoice records.
{% endhint %}

## Step 4 — Load Your Carrier Cost Rates

Go to Carriers → Cost Rates and enter your negotiated rates for each carrier. This is the foundation of BidBoost — the platform uses your cost rates to calculate proposed rates for prospects.

You'll enter rates using the spreadsheet-style grid. For each carrier and service you'll need:

- Weight breaks and corresponding rates per zone
- Effective date range for the rate set
- A nickname to identify the rate set (useful if you have multiple rate sets for the same carrier)

Once your rates are in, you can assign them to specific warehouses so the right rates are always used in the right bid.

For full details on loading and managing cost rates, see [Cost Rates](bidboost/cost-rates.md).

## Step 5 — Run Your First Bid

Go to Sales → Bid Center and click New Bid. You'll be guided through:

1. Selecting or adding a prospect
2. Choosing your bid type — PLD (shipment file), SKU, or No Data
3. Selecting your carriers and services
4. Applying your markup
5. Exporting your rate card

Your first bid should take about 10 minutes once your cost rates are loaded.

## Step 6 — Set Up Billing

Go to Billing and create your first billing cycle. Add your customers to a period, ingest your carrier invoices, apply your billing rules, and generate your first bill.

If you are new to Diversifi billing, start by connecting your carrier integrations or setting up email invoice ingest so invoices flow in automatically.

## Your First 30 Days — Checklist

Use this checklist to make sure you have everything set up correctly in your first month:

- [ ] Account profile complete
- [ ] Team invited with correct roles assigned
- [ ] WMS connected and syncing
- [ ] Carrier cost rates loaded for all active carriers
- [ ] Cost rates assigned to warehouses
- [ ] First bid created and exported
- [ ] Carrier invoices connected via integration or email ingest
- [ ] First billing cycle created
- [ ] Billing rules configured in Owlfred
- [ ] First bill generated and reviewed

## Need Help?

If you get stuck at any point, use the search bar at the top of this page — our AI will find the answer from our documentation instantly.

You can also reach your Diversifi account manager directly at [support@diversifi.ai](mailto:support@diversifi.ai).
