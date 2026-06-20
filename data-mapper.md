# Data Mapper

The Data Mapper is the AI-powered translation layer that converts raw data from your WMS or uploaded shipment files into Diversifi's standardized internal format. Every WMS system and every customer's shipment file uses different column names, units, and data structures — the Data Mapper figures out what everything means and normalizes it automatically.

## How It Works

When data comes into Diversifi — either from a WMS sync or from a manually uploaded PLD file — the Data Mapper reads the column headers and content, builds a mapping that translates the source fields to Diversifi's target fields, and applies any transformations required (unit conversions, format changes, enrichment).

- **Source fields** — what your file or WMS calls the data (e.g. "Ship Weight", "wt_lbs", "package_weight")
- **Target fields** — what Diversifi needs the data to be called internally (e.g. "total weight")
- **Transformations** — conversions applied during mapping (e.g. ounces to pounds, ZIP code formatting, carrier name normalization)

## Color Coding in the Data Mapper

When you view a mapping, fields are color coded to show how they were handled:

| Color | Meaning |
|-------|---------|
| 🟢 **Green** | Carried over directly — the source field mapped cleanly to the target with no transformation needed. |
| 🟡 **Yellow** | Transformed or enriched — the field was mapped but required a conversion or enrichment to match the target format. |
| ⚪ **Gray / Missing** | Not mapped — no source field could be matched to this target field. If it's a required field, this will affect data accuracy. |

## Required Fields

The Data Mapper has two hard-required fields for PLD (shipment file) uploads. Without these, shipments cannot be rated:

- **Destination ZIP code** — required for zone calculation and carrier coverage determination
- **Weight** — required for rate calculation. Must be in pounds or ounces (ounces are converted automatically).

Additional fields like tracking number, carrier, service, origin ZIP, and dimensions improve accuracy but are not strictly required. The more data you provide, the more accurate the bid output will be.

## AI Mapping Behavior

The Data Mapper uses AI to build the mapping each time it processes a new source. This means:

- The same file run through the Data Mapper twice may produce slightly different mappings — this is expected. The AI re-evaluates the mapping each time and may make slightly different decisions. Variance is typically small; in most cases the majority of runs produce an identical mapping, with occasional minor differences that don't significantly affect the output.
- If you need a consistent mapping for a recurring customer file, use the saved mapping feature to lock it in once it has been reviewed and confirmed.

{% hint style="info" %}
**Using existing mappings:** Once a mapping has been reviewed and confirmed as accurate, you can save it and reuse it for future uploads from the same source. This bypasses the AI mapping step and ensures consistency for recurring files.
{% endhint %}

## Common Data Issues

| Issue | How Diversifi handles it |
|-------|--------------------------|
| **Leading apostrophe on ZIP codes** | Some exports (particularly from Excel) add a leading apostrophe to ZIP codes to prevent Excel from stripping leading zeros. Diversifi removes these automatically during mapping. |
| **Weight in ounces** | The Data Mapper detects weights in ounces and converts them to pounds automatically. Always verify the weight unit is detected correctly after mapping. |
| **Missing leading zeros on ZIP codes** | Five-digit ZIP codes with leading zeros (e.g. 01234) may lose the leading zero in some files. The Data Mapper normalizes these — verify destination ZIP codes in the output. |
| **Raw carrier names** | WMS systems often output carrier names in raw API format (e.g. "fedex_ground" instead of "FedEx Ground"). The Data Mapper enriches these to display names where possible. |
