# High-SNR Twitter — Agent Operating Rules (draft)

Rules for the agent assisting with Twitter/X curation. These are process rules;
content rules (block/mute criteria) are being derived live in review sessions.

## R1 — "5 by 5" sync rule (feed review)

When reviewing the live timeline together:

1. Show exactly **5 tweets per batch**, in on-screen order.
2. Only present tweets that are **currently rendered on the user's screen** — never a
   backlog built from DOM residue of earlier scroll positions.
3. After each batch, **stop and wait** for the user's verdicts before scrolling or
   loading more.
4. Before the first batch, confirm with the user that they see the same 5
   (same tab — For you vs Following — and same scroll position).
5. If the user can't see an item, the batch is invalid: scroll back, re-sync, redo.
6. If we're not on the same page, the review is meaningless — stop and re-sync instead
   of pressing on.

*(Origin: user reported not seeing @_Liso_ in the feed after agent presented a 10-item
table compiled from accumulated DOM state.)*

## R2 — Explicit refresh before each batch (page re-sync)

Before each review batch, **hard-refresh the browser** and start from the top of the
page. Only tweets that (re)load after the refresh and are on screen may be presented.
Never present DOM residue from earlier scroll positions.

Caveats accepted by user:

- On `For you`, every refresh **reshuffles** the timeline (non-deterministic order) —
  a refresh guarantees a *shared view*, not the *same content* as last batch.
- On `Following`, order is chronological and stable across refreshes — better for
  strict same-page review.
- Freshly loaded items = the only items under discussion. Everything else is out of
  scope until re-encountered.

*(Origin: user — "i bet every time we may need to explicitly refresh the browser,
otherwise difficult to stay on the same page.")*

## C-rules — Content criteria (block vs mute tiers)

### C1 — Profanity × snark register

- **Mild profanity alone** (occasional curse, casual register) → **Mute** tier; agent decides.
- **Profanity co-occurring with quote-tweet sneering / mocking tone / engagement-bait** →
  **Block** tier.
- Before blocking, verify with the profile scan: open the account, confirm profanity
  across **multiple recent posts**, not a single quotable outlier. If verification is
  inconclusive → Ask tier (surface to user, don't act).
- Note evidence quality honestly when deciding ("2 of 3 visible posts crude" ≠ "constant
  swearing").
- Verified quote-sneer example: @josiah_arcanist — "how is this shit allowed" (re: @_catwu's
  OpenAI Core PM joining announcement) + "Dumbass discourse comes around…" (re: @sonicfields).
  Joined Aug 2024. Blocked 2026-11-05.

### C2 — Low-SNR amplifier (block tier)

Trigger = **all three**, evaluated over the account's trailing ~20 posts (firsthand
profile scan, like C1):

1. **Quote-reaction density ≥ ~50% (rough)** — quote-posts or bare reactions/replies
   carrying no artifact from the author. *(Lowered from ≥60% by user decision
   2026-11-05: "a rough 50% quotes are already red flag.")*
2. **Zero original artifacts** — no post links or shows anything the author
   made, found, or wrote: no repo, demo, paper, dataset, or analytical thread.
3. **Dominant register = reactive hype / hot-takes** — confident, unfalsifiable,
   evidence-free (engagement-farming shape).

⇒ **Block**. One or two original-artifact posts in the window **clears the flag**
(safety valve — genuine builders pass; pure reactors don't).

Corroborating, **never trigger**: hype lexicon ("alpha drop", "permanent underclass",
"slaughterbots", "singularity", "free market win"…) and self-description bios
(e.g. "Today is a great day to grow"). These may raise confidence and trigger a
second look; they can never authorize an action alone.

Do **not** key this rule to posting cadence (low-SNR accounts often post slowly).

Verified against @corbtt — 13 posts sampled (Aug–Nov 2026): 6/13 direct quotes
(7/13 counting discourse-reaction replies), 0 original artifacts, own-original posts drew
1–3K views / 3–25❤ against 19.7K followers; only outlier (280❤, 14K views) was a quote
of someone else's work. Blocked 2026-11-05.

### C3 — No politics in the library (block tier)

User's stance: **zero politics in the feed, period.**

- **Trigger:** the account's regular feed carries recurring political/policy commentary —
  democracy theory, ballot measures, regulation of labs, wealth redistribution, partisan
  or culture-war discourse. A one-off passing mention adjacent to a tech topic does not
  fire this rule; recurrence does.
- Firsthand profile scan required; sample ≥ ~10 posts across recent weeks before acting.
- ⇒ **Block** tier (again per user: "no politics in my lib").
- Verified against @gfodor — ~25% of 16 sampled posts were political/policy (democracy
  point take, CA Prop 38 $4.2B ballot measure, "US should compel labs to open source
  last gen models", Anthropic/SpaceX "free shares" wealth-share take). Blocked
  2026-11-05. Also noted: very high cadence (103K+ posts) with duplicate reposts.

## Open questions / to be filled during review

- [ ] Block vs Mute vs Allow criteria (tiering)
- [ ] Paid/ad impressions handling
- [ ] Self-promo vs genuine content
- [ ] Unverified-rumor (leak) accounts
- [ ] What "verified" does and does not prove
- [ ] Verification recipe for funds/orgs before blocking (f.inc case)
