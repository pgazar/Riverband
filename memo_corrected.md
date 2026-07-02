# Q1 Distribution — Board Summary

*Prepared for board chair review. Figures computed directly from `partner_agencies.csv` (planned allocations, families served) and `distribution_log_q1.csv` (actual Q1 deliveries).*

We distributed **562,368 lbs** across 47 partner agencies in Q1. (Note: 812 lbs of this is logged to an agency name that doesn't match our roster — see Data Notes — so 561,556 lbs is confidently attributed to named partner agencies.)

## By county — lbs per family per month

| County | Planned | Jan | Feb | Mar | Q1 avg | vs plan |
|---|---:|---:|---:|---:|---:|---:|
| Harlan | 41.9 | 42.7 | 42.0 | 33.5 | 39.4 | -6.0% |
| Price | 39.5 | 40.0 | 38.8 | 31.1 | 36.6 | -7.3% |
| Ellis | 29.4 | 25.5 | 26.4 | 20.2 | 24.0 | **-18.4%** |

**Ellis is the most under-served county by a wide margin** — more than double the shortfall of Harlan or Price. The board chair's concern about Ellis is borne out directly in the Q1 numbers.

March was the weakest month for all three counties: every county's per-family delivery dropped sharply in March relative to January and February.

## Agencies furthest under allocation

| Agency | County | vs plan |
|---|---|---:|
| Ellis Senior Center | Ellis | -48.0% |
| New Hope Shelter | Ellis | -42.2% |
| Southside Church Pantry | Ellis | -39.8% |

All three agencies furthest under their planned allocation this quarter are in Ellis County. Ellis Senior Center received 10,862 lbs against a planned 20,886 lbs for the quarter — about half its target.

## Hub agencies

By families served monthly, the largest partner in each county is:

- **Ellis:** Ellis Rescue Mission (312 families)
- **Harlan:** First Baptist Pantry (314 families)
- **Price:** Price Head Start (338 families)

Note: the handbook defines a "hub" as an agency that informally forwards part of its allocation to smaller satellite pantries we don't deliver to directly. That forwarding isn't tracked in any data we have, so beyond the families-served figures above, we can't confirm from data which agencies function as true hubs.

## Recommended actions

1. **Prioritize the three most under-allocated Ellis agencies for review** — Ellis Senior Center, New Hope Shelter, and Southside Church Pantry. Per the handbook, any allocation change needs Marcus's review against current inventory before anything is committed.
2. **Investigate the Ellis delivery logging.** All 18 duplicate delivery records found in the Q1 export belong to Ellis County agencies, spread across all three trucks (see Data Notes). This looks like a systematic logging or export issue specific to Ellis stops — worth a targeted check by Marcus's team, not just a general route review. (Warehouse, trucks, and partner-agency delivery operations are Marcus's area per the handbook.)
3. **Resolve the "St Marks Pantry" record** (see Data Notes) before it's included in any agency's totals or used for an allocation decision.
4. **For the formula review:** Ellis serves 1,341 families on the lowest planned per-family allocation of the three counties (29.4 lbs, vs. 41.9 Harlan and 39.5 Price) — a structural gap that exists independent of the Q1 delivery shortfall and is worth the board's attention on its own.

*Context: Ellis is our highest Spanish-speaking-share county.*

## Data notes

Issues found in the raw delivery export, stated plainly rather than smoothed over:

1. **47 test rows excluded (46,953 lbs).** Every one is dated March 1, assigned to truck `T-99`, and logged at exactly 999 lbs — one per agency. This matches the handbook's note that T-99 is the warehouse's month-start scale/barcode calibration slot, not a real delivery route. Removed from all totals above. *Worth a one-line confirmation from Marcus's team.*
2. **18 duplicate delivery records excluded (12,356 lbs).** Same agency, date, weight, and truck, logged twice. Every one belongs to an Ellis County agency — none in Harlan or Price. Removing these is what produces Ellis's -18.4% figure (leaving them in would understate the shortfall at roughly -8%), so **before this is final, Marcus's team should confirm these are true duplicates and not two legitimate same-day deliveries.**
3. **Spelling variants merged for 3 agencies:** "Grace Fellowship" / "Grace Fellowsihp" → Grace Fellowship Church; "Mount Zion Food Pantry" / "Mt. Zion Food Pantry" → Mt Zion Food Pantry; "St. Paul Food Shelf" → St Paul Food Shelf. (Left unmerged, Mt Zion would falsely appear to be at -61.9%; combined, it's actually -6.5%, in line with the rest of Price County.)
4. **One unresolved agency name: "St Marks Pantry"** (812 lbs, one delivery, Feb 17). It matches none of our 47 roster agencies. Needs a person to identify it — typo, an unrostered partner, or a mis-loaded record — not a guess.
5. **The export's date coverage is clipped:** records span only the 2nd–27th of each month, with nothing on the 1st or the final days. That uniformity across all three months suggests the export window itself was clipped, not that deliveries paused. The true Q1 total is likely somewhat higher than 562,368 lbs — probably by a similar proportion across all counties, so it shouldn't change the county comparison, but treat the total as a floor rather than an exact figure.

---
*Please have Marcus's team confirm the T-99 and Ellis-duplicate explanations before this goes to the board — both are inferred from the delivery data and the handbook, not confirmed directly with the warehouse.*
