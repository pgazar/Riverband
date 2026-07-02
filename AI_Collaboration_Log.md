# AI Collaboration Log — Riverbend Food Alliance Take-Home

## Purpose
This log tracks how Claude was used throughout Task 1, to support the Task 2 write-up.
It records: prompts used, Claude's role at each step, decisions made, what was accepted vs. changed, and why.

---

## Pre-Task Setup

**Time budget:** 2 hours for Task 1 (self-imposed, tighter than the platform's stated 3-hour allowance), 1 hour for Task 2.

**Environment clarification needed:** whether Task 1 runs in a live Claude Project/connector environment provided by the assessment platform, or is a text-based inbox with Claude used as an external aid.

**Framework applied throughout:** Discover & Scope → Build → Enable & Hand Off (matches Claude Corps' own workflow language and the resume framing already used in the fellowship application).

**Fellowship evaluation lens kept in view:**
- Visible iterative use of Claude (prompts + refinements shown, not just final output)
- Critical judgment — moments where Claude's output was corrected, pushed back on, or rejected
- Clear handoff quality (would a non-technical teammate understand this?)
- Honest self-representation — no overclaiming of complexity

---

## Handbook Review
Read in full before drafting anything. Key corrections it made to assumptions
the *old* triage prompt was operating on:
- Drop-off hours are Tue/Thu/Sat 9am-1pm, not "every day 8am-6pm" (old prompt's
  invented hours were being sent to every individual donor).
- Only Marcus can confirm dock space, short-dated product, or partner
  allocations — explains both board-meeting incidents directly.
- Press/reporters/partnership pitches -> Diane, always.
- Needs list changes monthly and must not be recited from memory.
- Food assistance: no gatekeeping, send find-food link + ask ZIP, escalate
  acute cases to intake line, reply in sender's language.

## Email 1 — Marcus Chen: rewrite the donate@ triage prompt
**Ask:** rewritten `triage_prompt.md` (JSON-only, Haiku, 8 fixed categories,
6 fixed routing targets), a 1-page evaluation note, and `corrections.csv`
re-triaging 6 flagged failures.

**Diagnosis (before touching the prompt):** read all six failure examples
against Marcus's two incident stories (false allocation promise; "bring it
anytime!" sent to a corporate donor) to find root causes rather than just
reformatting to JSON. Found four failure patterns:
1. Draft language fabricating commitments (turnaround times, allocation
   confirmations, a nonexistent attachment, an invented intake process).
2. No corporate-vs-individual distinction, which is the likely cause of the
   "Seriously?" incident.
3. No routing logic at all in the old prompt.
4. Multi-intent emails (Jen Park's) only partially answered.

**Design principle adopted:** the model may draft warmly but must never
commit the org to anything unconfirmed; default to human routing over
`auto_ok` whenever uncertain. This single rule addresses both real incidents
Marcus described, so I treated it as the spine of the new prompt rather than
a footnote.

**Corrections.csv reasoning (judgment calls worth documenting):**
- `jen` — marked **not urgent** despite the "before May 15" deadline: it's a
  forward date, not an imminent same-day/EOD deadline like the other urgent
  cases, so I didn't want to over-flag routine scheduling as urgent and dilute
  the signal for genuinely time-critical items (e.g., Kevin's Wednesday
  liquidation deadline). Category picked as `volunteer_inquiry` over
  `food_drive` since both intents route to Priya anyway per the handbook, so
  the category choice doesn't change the outcome here — but the draft must
  still answer both questions.
- `ana` — marked **not urgent**: "this month is difficult" reads as ongoing
  hardship, not the handbook's "acute, no food today" bar for escalation.
  Routed to `auto_ok` because the correct response is fully standardized by
  the handbook (find-food link + ask ZIP, in Spanish) — nothing is being
  promised that isn't already true.
- `sarah` — kept `auto_ok`: plain individual donation, no confirmation needed
  beyond accurate hours/accepted-items info.
- `kevin`, `pastor_dan` — routed to `marcus`, matching the handbook's explicit
  "only Marcus confirms this" rule, even though the old prompt's category and
  urgency calls were already correct — the failure was entirely in the draft
  content and missing routing, not the classification.

**Files produced:** `triage_prompt.md`, `evaluation_note.md`,
`corrections.csv`.

**Live test results (run by the person in a separate Claude Project, per
copilot workflow — I evaluated, did not generate, this run):**
Tested the prompt against all 40 rows of `inbox_sample.csv`. Findings, in
priority order:
1. **Bug I caught that the self-report missed:** `individual_food_donation`
   items with ambiguous accept-status (produce, sparkling water — S07, S09,
   S11, S13) were routed `auto_ok` while their drafts said "someone will
   follow up to confirm" — a real contradiction, since `auto_ok` means no
   human reviews it. This is the same failure shape as the original board
   incidents: a promise with nobody assigned to keep it. Needs a general
   rule: any draft that defers to "someone will follow up" must route to a
   human, not `auto_ok`.
2. **Self-flagged and confirmed:** urgency rule over-triggers on any stated
   deadline regardless of distance (S24's "by May 15" flagged equally urgent
   as S28's "EOD Wednesday"). Same root cause also explains S33–S35 (press
   inquiries "this week") getting flagged urgent — wider impact than just
   the volunteer category. Fix: qualify to a near-term window (~3-5 business
   days).
3. **Self-flagged and confirmed:** missing-item deliveries were marked
   urgent by the model (matching the handbook) but the prompt's literal
   urgency criteria don't list "missing item" — only damaged/expired/wrong
   product. Model followed handbook intent over prompt text, which is
   fragile for future editors. Needs explicit addition to the prompt.
4. **Confirmed gap:** produce and sparkling water aren't on the accepted or
   rejected items list; came up 4 times in 40 emails, not a rare edge case.
5. **Found independently, not asked for:** all four corporate-donation
   sample emails (S02–S05) have subject lines that don't match their body
   content (different products/quantities). Model correctly triaged off
   body text every time. Worth flagging to Marcus as a data-quality pattern,
   parallel to the T-99 finding in Diane's task.
6. **Coverage gap in the test itself:** no sample email came from a known
   major-donor domain, so the handbook's most sensitive rule (never
   reference the donor table, route to relationship owner) remains
   unverified. Flagged for the next regression pass rather than assumed to
   work.

**Two final decisions closed out after the live test:**
- Date dependency for the urgency fix: rather than add a manual date-entry
  step (friction across ~1,200 emails/month, easy to skip/mistype), the
  prompt now uses the current date Claude already has access to in every
  conversation, falling back to "not urgent" if unavailable. Flagged for a
  live spot-check before trusting it, since I can't independently verify
  the Project's context carries this the same way a plain chat does.
- `intake_line` was a routing target Marcus specified but the original
  design never used. Per the handbook's acute-need process, urgent
  `food_assistance_seeker` emails now route to `intake_line` instead of
  `auto_ok`. Decided rather than asked, since Marcus is heading into a
  board meeting and a small, reversible design call is better delivered
  as "here's what I did, flag if you'd rather it differently" than as an
  open question adding to his load. Both changes applied directly to
  `triage_prompt.md` (on disk via the Filesystem connector) and
  documented in `evaluation_note.md`.

**Process note worth keeping for Task 2:** made a real tool-use mistake here
— first attempt to edit the file on the person's Mac used `terminal:write_file`,
which silently wrote to Claude's own sandboxed environment instead of the
real filesystem connector (`Filesystem:edit_file`/`Filesystem:write_file`).
Caught it by checking `Filesystem:list_directory` before assuming the earlier
write had worked, rather than trusting my own "Successfully wrote" message.
Corrected and told the person directly rather than letting it pass quietly.

**Not yet done:** Marcus's second email (cost estimate).

## Email 2 — Priya Raman: volunteer confirmation flow architecture
**Ask:** an architecture sketch only (explicitly told not to build), as
`architecture.html` with SVG/Mermaid, covering signup -> roster -> reminder
texts -> Claude's role -> a Monday-morning confirmation signal. Mark where
MCP fits, if relevant. Diane will ask about ROI — need to quantify.
*(in progress — see next steps)*

## Email 3 — Diane Okafor: fact-check the Q1 board memo
**Ask:** correct `draft_memo.md` against the raw `partner_agencies` and
`distribution_log_q1` files, output `memo_corrected.md`, keep structure,
surface data hygiene issues rather than quietly fixing them.

**Process:** used pandas (not a from-scratch Claude Project re-summarization)
to independently recompute every number in the draft, rather than asking
Claude to "check" the draft against the files conversationally — this
avoids repeating whatever error pattern produced the original draft.

**What I found, in order of impact:**
1. **The Q1 total (621,677 lbs) exactly matched total-including-47-fake-
   test-rows.** The handbook mentions a `T-99` truck ID used for
   scale/barcode testing at month-start that "shows up in exports but isn't
   real deliveries" — I checked the log for it and found exactly 47 rows,
   999 lbs each, all dated March 1, one per agency. 47 x 999 = 46,953, which
   is exactly the gap between the draft's total and the real one
   (574,724 lbs). This one artifact also skewed March upward for every
   county, which is why the draft concluded "Ellis is over plan" and "March
   was the strongest month" — both false once removed.
2. **Agency name variants inflated apparent under-allocation.** Manually-
   typed truck logs had "Grace Fellowship"/"Grace Fellowsihp" and "Mount
   Zion Food Pantry"/"Mt. Zion Food Pantry" as separate strings from their
   roster names, so their real deliveries were being split and undercounted
   against a single agency. Once merged, Mt Zion (-61.9% in the draft) is
   actually only -6.5%; Grace Fellowship (-32.9%) is actually -5.3%.
3. **"St Marks Pantry" (recommended in the draft for an allocation increase)
   isn't in the 47-agency roster at all** — a single 812-lb delivery with
   no clear match to an existing agency name (checked against St Andrew, St
   James, St Paul — none are close). Flagged rather than guessed at.
4. **The "hub agencies" claim didn't hold up**: the three named agencies
   have below-median families-served counts, and the handbook confirms
   hub-forwarding isn't tracked anywhere, so the claim wasn't verifiable
   from data. Flagged as unsupported rather than repeated.
5. Ellis's families-served figure was corrected from 1,890 (unexplained in
   the draft, doesn't match any grouping in the roster) to 1,341 (actual
   roster sum).

**Net effect on the story:** the original draft concluded the board chair's
Ellis concern "doesn't show up in the numbers." The corrected numbers show
the opposite — Ellis is the most under-plan county, and its three most
under-allocated agencies are all real, all in Ellis. This is the kind of
reversal that's easy to miss if you fact-check a draft by re-asking Claude
to review its own summary instead of recomputing from the source files
directly — worth calling out explicitly in the Task 2 writeup.

**File produced:** `memo_corrected.md`.

**What I'd verify if this weren't time-boxed:** asked Diane's memo to flag
the T-99 exclusion and the St Marks Pantry anomaly for Marcus to confirm
before board day, since both touch his team's data entry — I didn't treat
my own correction as unquestionable given I can't independently confirm
warehouse process.

## Email 4 — Budget follow-up
*(pending)*

---

## Design Decisions
- Adopted "never let a draft promise what a human hasn't confirmed" as the
  organizing principle for the triage prompt, since both real incidents
  Marcus described trace back to exactly that failure.
- Chose to keep routing conservative (default to a human) rather than
  optimizing for `auto_ok` coverage, even though that means more emails land
  on staff desks — matches the org's actual risk tolerance (small team, two
  recent trust-damaging mistakes) better than maximizing automation.

## Errors / Corrections
- Used the wrong file-write tool on the first attempt to save
  `triage_prompt.md` to the person's Mac (`terminal:write_file` instead of
  the real `Filesystem` connector). Caught by checking the directory listing
  rather than trusting the tool's own success message. Corrected immediately
  and disclosed directly.
