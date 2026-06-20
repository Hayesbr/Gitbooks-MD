# Markups & Surcharges

This article explains everything you need to know about how markups work and how to use the markups screen effectively.

## How Markups Work

The markups screen is one of the most important parts of BidBoost. It is where you set your margin, compare carriers, and make sure you are pricing competitively before sending a rate card to a prospect.

A markup is the percentage or dollar amount you add on top of your cost rates to produce the rate you charge the prospect. For example, if your cost rate for a 5 lb FedEx Ground shipment to zone 4 is $8.50 and you apply a 20% markup, the prospect sees $10.20.

Your actual cost rates are never visible to the prospect. They only ever see the rate after your markup has been applied.

**The markup formula** — For every weight and zone combination, Diversifi calculates the proposed rate using the following logic:

1. Start with the base rate from your cost rates.
2. Add any applicable surcharges — fuel, residential, additional handling.
3. Apply your markup percentage to the total.
4. Compare against your minimum dollar markup if one is set.
5. Whichever is greater — the markup percentage result or the minimum dollar amount — becomes the proposed rate.

## The Speed Tier View

Your shipments are organized into speed tier groups on the markups screen. Each group shows you where the packages from the prospect's file went and what the average cost per package is for each carrier and service in that group.

- **Next Day** — shipments where a next day service wins
- **2–3 Day** — shipments where a 2 to 3 day service wins
- **4–5+ Day** — shipments where a slower ground service wins
- **Unrated** — shipments where a speed tier could not be determined. Shown at the bottom for visibility but excluded from rated results.

Every package in the file is accounted for. If you submitted 1,000 packages, you will see the exact count in each bucket.

## The Winning Carrier Badge

Each speed tier group shows a badge identifying the winning carrier and service — the one with the lowest average cost per package after all markups are applied. This badge updates in real time as you adjust your markups. As you increase the markup on one carrier, another carrier may become cheaper and take the winning badge. This is intentional — it shows you the exact point where your pricing decisions affect which carrier wins the business.

Use the winning badge to:

- Confirm your preferred carrier is winning before you export
- Identify whether your markup on one carrier is too high and pushing shipments to a competitor
- Make sure your pricing strategy produces the outcome you expect for the prospect

## Adjusting Markups

**Individual carrier and service markups** — Use the slider next to each carrier and service to set the markup for that specific service. As you move the slider, the average cost per package updates immediately. The slider takes precedence over any carrier-wide markup you have set: if you set a carrier-wide markup of 15% and then move an individual slider to 20%, that service will use 20%.

**Carrier-wide markup** — Enter a percentage in the carrier-wide markup input field to apply the same markup across all services for that carrier at once. The field updates to reflect the weighted average across all services if you subsequently adjust individual sliders.

**Quick Actions** — For blanket markups across all carriers or all services at once, use the Quick Actions panel:

- Apply a percentage markup to all carriers
- Apply a percentage markup to all services within a speed tier
- Apply AI recommendations (see below)

Quick Actions are useful when you want to start with a baseline markup across everything and then fine-tune individual carriers or services.

## Pricing Limits

Your account Owner can configure pricing limits that set a floor on how low your markups can go. Pricing limits protect your margin by preventing a sales rep from accidentally pricing below cost or below your minimum acceptable margin.

If you enter a markup that would result in a rate below the pricing limit, you will see a warning identifying which services are affected. You can review the warning and either adjust your markup or confirm you want to proceed. Pricing limits can be set as a minimum markup percentage, a minimum dollar amount per package, or both — if both are set, the platform uses whichever produces the higher rate.

## Fuel Surcharge

The fuel surcharge is a percentage added on top of the base rate to account for carrier fuel costs. Toggle it on to include it in the prospect's proposed rates. The percentage is configured in your carrier configuration settings; when toggled on, it applies to all carriers selected in the bid that have a fuel surcharge configured.

{% hint style="info" %}
Fuel surcharge applies to the base rate **before** your markup is calculated:
(Base rate + Fuel surcharge) × Markup percentage = Proposed rate
{% endhint %}

## Residential Surcharge

The residential surcharge is an additional fee carriers charge for deliveries to residential addresses. Toggle it on if the prospect's shipments include residential deliveries and you want to include this fee in the proposed rates.

Not all carriers charge the same residential surcharge. The amount is configured per rate set in your carrier configuration settings.

When the residential surcharge toggle is on, Diversifi adds the surcharge to all applicable rates. Services that are already priced as residential delivery are excluded, because the residential cost is already built into their base rates.

Carriers charge different residential surcharges for Ground and Air services, so you enter a separate Ground and Air residential rate for each rate set in the carrier configuration screen. Diversifi automatically applies the correct rate based on whether each service is Ground or Air.

## Additional Handling

Additional handling fees apply to packages that exceed certain size or weight thresholds. Toggle additional handling on if the prospect's file includes oversized packages and you want to include this fee in the proposed rates.

## Minimum Dollar Markup

In addition to a percentage markup, you can set a minimum dollar amount per package. This ensures that even on very low-cost shipments you always make at least a minimum dollar margin.

For example, if your minimum dollar markup is $2.00 and your percentage markup on a $5.00 shipment would only produce $1.00 of margin, the platform will use $2.00 instead. The minimum dollar markup is configured by your account Owner in the pricing limits settings.

## AI Recommendations

The AI recommendation feature suggests a markup level for each carrier and service based on market data. The recommendation is calculated as 5% above your cost or 5% below market rates — whichever produces the higher proposed rate.

To apply AI recommendations, click Quick Actions and select Apply AI Recommendations. You can apply them to all carriers at once or review and apply them individually. AI recommendations are a starting point — review them before exporting and adjust based on your knowledge of the prospect and the competitive situation.

## Restore to Default

Click Restore to Default to reset all markups back to their default state. If a minimum pricing limit is configured, the default will be set to that minimum rather than 0%. If no pricing limit is set, the default is 0%.

## Common Questions

**Why is a carrier winning that I didn't expect?** Check the average cost per package for each carrier in that speed tier. The winning carrier is always the one with the lowest average cost per package after all markups are applied. If a carrier you don't want to win is winning, try increasing its markup until your preferred carrier takes the winning badge.

**Why is my carrier-wide markup not updating after I move a slider?** When you move an individual slider, it takes precedence for that service. The carrier-wide markup field updates to show the weighted average across all services for that carrier, reflecting the mix of your carrier-wide markup and any individual slider adjustments.

**Can I lock a carrier out of winning?** Not directly — but you can increase the markup on a carrier high enough that it never wins any speed tier group. The winning badge will move to the next cheapest carrier.

**What does it mean when a service shows in the Unrated group?** Unrated shipments are ones where Diversifi could not determine a speed tier from the data in the prospect's file. This can happen when carrier or zone data is missing for a particular shipment. Unrated shipments are shown for visibility but do not affect the rated results above them.

**Why do my KPI totals not add up to my full file?** Check the Unrated count at the bottom of the screen. Unrated shipments are excluded from the KPI calculations since they do not have a confirmed rate. The rated shipment count plus the unrated count should equal your total file size.
