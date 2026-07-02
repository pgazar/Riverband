# Q1 Distribution — Board Summary (CORRECTED)

*Diane Okafor — for board chair review*

We distributed **574,724 lbs** across 47 partner agencies in Q1. (The original
draft's figure of 621,677 lbs included 47 rows of test data from the
inventory system — see Data Hygiene note below. That's the single biggest
correction in this memo, and it changes the story on Ellis.)

## By county — lbs per family per month

| County | Planned | Jan | Feb | Mar | Q1 avg | vs plan |
|---|---:|---:|---:|---:|---:|---:|
| Harlan | 41.9 | 42.7 | 42.0 | 33.5 | 39.4 | -6.1% |
| Price | 39.5 | 40.0 | 38.8 | 31.1 | 36.6 | -7.4% |
| Ellis | 29.4 | 30.2 | 28.9 | 22.2 | 27.1 | -7.9% |

**This reverses the original draft's conclusion.** All three counties are
under plan for Q1, and **March — not the strongest month, but the weakest**
for every county. Ellis is the furthest under plan of the three, which
directly supports the board director's concern rather than contradicting it.

## Agencies furthest under allocation

| Agency | County | vs plan |
|---|---|---:|
| Ellis Senior Center | Ellis | -48.0% |
| New Hope Shelter | Ellis | -42.2% |
| Southside Church Pantry | Ellis | -36.4% |
| Lincoln HS Backpack Program | Harlan | -16.2% |
| Price Head Start | Price | -15.9% |

**All three of the most under-allocated agencies are in Ellis County.** The
original draft's list (Mt Zion Food Pantry -61.9%, Ellis Senior Center
-43.2%, Grace Fellowship Church -32.9%) was distorted by unmerged spelling
variants in the delivery log — see below. Mt Zion and Grace Fellowship are
actually close to plan (-6.5% and -5.3%) once their deliveries are correctly
combined; Ellis Senior Center's shortfall is real and, if anything, slightly
larger than originally reported.

## Hub agencies

The original draft named Open Door Mission, Northgate Church Pantry, and
Bethel AME Food Ministry as our "largest partners by families served." That's
not supported by the data — those three agencies report 118, 102, and 138
families/month respectively, below the county medians (the largest by
families served are actually Price Head Start at 338 and First Baptist
Pantry at 314). Per the handbook, hub-to-satellite forwarding isn't tracked
in any system, so hub status can't be confirmed or ranked from this data —
recommend removing this section from the board version rather than stating
an unverified claim, or checking with Marcus/Priya directly if the board
needs it.

## Recommended actions

1. **Prioritize the three Ellis agencies above for allocation review**
   (Ellis Senior Center, New Hope Shelter, Southside Church Pantry) — the
   data supports these, not "St Marks Pantry" from the original draft, which
   is not one of our 47 partner agencies (see Data Hygiene).
2. Ask Priya to audit the Ellis delivery routes — the handbook notes Ellis is
   our longest run (~50 min each way) and the stops most likely to get
   short-loaded when a truck is tight on time or weight. That operational
   detail lines up with what the corrected numbers show.
3. Note for the formula review: Ellis serves **1,341 families** (not 1,890 —
   corrected, see Data Hygiene) on the lowest per-family planned allocation
   of the three counties (29.4 vs. 41.9 Harlan, 39.5 Price). That gap exists
   independent of the Q1 delivery shortfall and is worth the board's
   attention on its own.

*Context: Ellis is our highest Spanish-speaking-share county. Routes and
truck schedules are owned by Priya.*

---

## Data hygiene issues found (per your request, flagging rather than papering over)

1. **47 test rows inflated the total by ~47,000 lbs.** The delivery log
   contains 47 rows on truck `T-99`, all dated March 1, all exactly 999 lbs —
   one per partner agency. These are scale/barcode-reader test entries the
   warehouse team runs at month-start, not real deliveries. They accounted
   for the entire gap between the original draft's total (621,677 lbs) and
   the corrected total (574,724 lbs), and skewed March — and therefore
   Ellis's standing — upward in the original draft.
2. **Agency names are entered by hand at the truck and aren't consistent.**
   I found and merged: "Grace Fellowship" / "Grace Fellowsihp" →
   "Grace Fellowship Church"; "Mount Zion Food Pantry" / "Mt. Zion Food
   Pantry" → "Mt Zion Food Pantry"; "St. Paul Food Shelf" → "St Paul Food
   Shelf." Unmerged, these variants each looked like a separate
   under-performing agency, which is most of why Mt Zion and Grace
   Fellowship looked far worse in the original draft than they actually are.
3. **One delivery doesn't match any partner agency.** 812 lbs went to "St
   Marks Pantry" on Feb 17 (truck T-14) — this name isn't in the 47-agency
   roster and isn't a clear misspelling of an existing one (we do have a
   St Andrew, St James, and St Paul, but no St Mark). Worth confirming with
   Marcus/the warehouse team whether this is a new/non-partner recipient or
   a data entry error, since it's currently sitting outside any tracked
   allocation.
4. **The families-served figures come from the roster (self-reported by
   agencies), not an independent count** — if any agency's number is stale,
   the per-family math shifts accordingly. Worth a periodic refresh cadence
   if that's not already happening.

*Corrected against `partner_agencies.csv`/`.xlsx` and
`distribution_log_q1.csv`/`.xlsx` — please have Marcus spot-check the
T-99 exclusion and the St Marks Pantry entry before this goes to the board,
since both come from his team's data.*
