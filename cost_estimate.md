# Donate@ Triage — Monthly Cost Estimate

**Short answer: about $3/month** to run the triage (roughly $4–5/month during the Nov–Dec holiday spike). Call it **~$40/year**.

## Assumptions (stated plainly)

- **Model:** Claude Haiku 4.5, at its current rate of $1 per million input tokens / $5 per million output tokens.
- **Volume:** ~1,200 emails/month normally, ~1,800 in Nov–Dec (both from the team handbook).
- **Per email, the system reads:** the triage instructions (~1,500 tokens) + the incoming email (~200 tokens), and writes back the JSON reply (~180 tokens, including the short draft).
- **That works out to ~2.6 cents per 10 emails** — about a quarter-cent each.

## One lever worth knowing

Because the same triage instructions are sent on every email, turning on "prompt caching" (a built-in feature) would cut this roughly in half — to about **$1.50/month**. Not necessary at this scale, but it's there if the volume ever grows.

## Honest caveat

This is an estimate based on typical email lengths — a month full of unusually long emails would push it up somewhat, but even doubling the estimate keeps it under $10/month. The cost is not the thing to worry about here; it's small enough that the real question for Diane is whether the triage is *accurate and safe*, not whether it's affordable.

---

*Pricing confirmed against Anthropic's current published Haiku 4.5 rate as of July 2026. Token estimates are approximate and based on the length of the triage prompt and the email samples provided.*
