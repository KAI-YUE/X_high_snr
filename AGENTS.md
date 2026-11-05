# AGENTS.md — X High-SNR (Twitter filter)

Mission: curate the owner’s X/Twitter feed for high signal-to-noise. Block or
mute accounts per the rulebook; log every decision. Personal project, single
maintainer (KAI-YUE), solo workflow on `main`.

## Working rules

- **5-by-5 review**: only what is on screen, in on-screen order, 5 items per
  batch; wait for the user’s verdicts; never present DOM residue.
- **Refresh per batch** (`https://x.com/home`); `For you` reshuffles each load —
  treat a refresh as a resync, not as preserving content. No `End` key (it jumps
  and unmounts); small `PageDown` steps only.
- **Verify before acting**: open the account’s profile and scan ≥10 posts before
  any mute/block. For-you impressions and follower counts are not evidence.
- **Log everything** in `decisions.md` (date, account, action, user-supplied
  reason, what was verified). Rules live in `PRINCIPLES.md`; decisions are
  examples, not rules.
- **Tiering**: mild/edge-cases → mute; clear violations → block; never act on
  unverified gut alone.
- **Language**: English only.

## Files

| File | Purpose |
|------|---------|
| `PRINCIPLES.md` | Rulebook. R-rules (review process) and C-rules (block/mute criteria) |
| `decisions.md` | Per-account action log with reasons |
| `.gitignore` | Excludes raw capture scratch (`*.yml`, `.playwright-mcp/`) |
| `.playwright-mcp/` | Raw browser captures — kept locally, gitignored |

## Resume checklist

1. Read this file, then `PRINCIPLES.md`, then skim `decisions.md`.
2. Browser: drive the logged-in X session via the Playwright MCP (Chrome profile
   `/home/kyue/.cache/pw-x-profile`). If the profile is locked, the user must
   close their own Chrome on it first.
3. Acting on an account: profile → **More** (top-right of header) → **Block** →
   confirm dialog. Reversible via the same menu (“Unblock”).
4. New rules: propose → user approves → append to `PRINCIPLES.md` → log example in
   `decisions.md` → `git add && commit && git push`.
5. Repo: `git@github.com:KAI-YUE/X_high_snr.git` (SSH; the stored HTTPS token was
   stale — HTTPS auth fails; use SSH).
