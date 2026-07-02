# Evaluating the new triage prompt — one page

## Why the old one failed (in one line)
It had no rule against making promises it couldn't back up, no format
requirement, and no real routing logic — so a friendly, well-meaning model
did what friendly, well-meaning people sometimes do under-informed: it said
yes on the org's behalf.

## How I'd test it before trusting it

**1. Regression set (do this first, costs nothing but time).**
Run the six flagged examples plus the ~40 rows in `inbox_sample.csv` through
the new prompt and check each output against three questions:
  - Is `category` right, especially corporate-vs-individual and
    partner-request-vs-general (the two boundaries that caused real damage)?
  - Is `route_to` conservative — human review whenever the draft could commit
    the org to anything?
  - Does the `draft` avoid promising quantities, dates, allocations, or
    inventing policy?

This is cheap to re-run every time the prompt changes, so it should become a
standing regression test, not a one-time check.

**2. Adversarial/edge cases worth adding to that set over time:**
  - An individual claiming an unusually large donation (tests the
    corporate/individual boundary).
  - A partner agency email that *sounds* routine but contains a food-safety
    complaint (tests that "partner request" doesn't default to low-urgency).
  - A multi-intent email like Jen Park's (tests that nothing gets dropped).
  - A known major-donor domain emailing about something unrelated to the
    relationship (tests that routing doesn't leak internal donor info into a
    draft).

**3. What "passing" looks like.**
Not 100% perfect drafts — a first-pass triage tool doesn't need to be
perfect, it needs to fail *safely*. The bar is: it should never auto-send a
commitment it can't verify. A wrong category that still routes to a human is
a minor annoyance; a wrong category that auto-sends a false promise is the
incident we're trying to prevent. I'd weight evaluation accordingly —
grade "safety of the routing decision" as more important than "polish of the
wording."

**4. Ongoing monitoring, once it's live.**
Ask the volunteer to keep flagging bad outputs the way they already did for
this batch (that's exactly how we caught these six). Feed new flagged
examples back into a running `failure_examples.md` so the prompt — and this
regression set — improves over time instead of being a one-time fix.

## What I did for this handoff
I re-ran the six flagged emails against the new prompt's logic by hand and
recorded the corrected category/urgency/routing in `corrections.csv`, so
there's already a working answer key to test against once the new prompt is
pasted into the Project. I then ran the full prompt against `inbox_sample.csv`
and revised it based on what that surfaced. Two follow-on decisions worth
your visibility:

**Date handling for the urgency rule.** The "is this deadline within 3-5
business days" logic needs to know today's date to work at all. Rather than
add a step where the volunteer types today's date into every triage — an
easy thing to skip or mistype, and friction on ~1,200 emails/month — the
prompt now tells the model to use the current date it already has access to
automatically in every claude.ai conversation, and falls back to "not
urgent" if that's ever unavailable. Worth a 30-second live check (ask the
Project "what's today's date?") before trusting this in production.

**`intake_line` was an unused routing target.** The original 6 routing
targets included `intake_line`, but nothing in the first draft ever routed
there — `food_assistance_seeker` always defaulted to `auto_ok`. The handbook
says acute food-assistance cases should reach the intake line for a same-day
call, so urgent `food_assistance_seeker` emails now route to `intake_line`
instead of `auto_ok`; non-urgent ones still go `auto_ok` with the standard
find-food-link reply. Flagging this as a decision made, not a question —
happy to change it if you'd rather it work differently.
