---
title: "Trying to Become an OpenClaw Contributor: Five Attempts, One Decision Gate"
date: 2026-09-08 11:20:00 +08:00
categories:
  - engineering
tags:
  - openclaw
  - open-source
  - code-review
  - clawsweeper
  - retrospective
  - ai-assisted
toc: false
---

In mid-2026 I spent several weeks trying to land a first merge into [OpenClaw](https://github.com/openclaw/openclaw) — the self-hosted multi-channel AI gateway people jokingly call the “lobster.” I wanted a real code contribution, not a docs-only drive-by.

I did not get that merge. I did get a clearer picture of how a high-throughput, bot-heavy OSS project actually absorbs (or deflects) outsider patches, plus a short personal reply from [Peter Steinberger](https://github.com/steipete) on the first PR. This post walks through **five attempts**, how AI helped across the whole loop, and why the last PR stalled on a product decision rather than missing tests.

![Cover: a small hermit crab walking five stepping stones](/assets/img/posts/openclaw-contributor-journey-cover.png)

---

## How I worked (with AI)

OpenClaw’s issue tracker moves fast — thousands of open items, heavy labeling, and an automated reviewer called **ClawSweeper**. Searching by hand is noisy. I leaned on an AI coding agent for more than triage.

My workflow was roughly:

1. Sync my fork to `openclaw/openclaw` `main`.
2. Ask the agent to **scan labeled issues** (`queueable-fix`, `fix-shape-clear`, `source-repro`, avoid `linked-pr-open` / `no-new-fix-pr`) — this is the “review vulnerabilities / find fixable defects” step, not a security exploit hunt.
3. Filter for bugs I could **reproduce on Windows** with unit tests or a small Control UI check.
4. Prefer narrow owner boundaries (one helper, one UI index, one dependency list) over cross-process policy rewrites.
5. Have the agent **draft the patch, add tests, and run the focused Vitest shards**; I steered the goal, checked the diff, and decided when to open, rewrite, or close a PR.

So the honest version is: AI did most of the mechanical engineering. I did the judgment calls — which bug to chase, when a review loop had grown past a first contribution, and when to walk away.

---

## Five attempts on a timeline

![Five OpenClaw contribution attempts from July to September 2026](/assets/img/posts/openclaw-five-attempts-timeline.svg)

### 1) Nested `rg`/`grep` search summaries — [#113401](https://github.com/openclaw/openclaw/issues/113401) / [PR #114484](https://github.com/openclaw/openclaw/pull/114484)

**Bug.** Exec tool display wrapped an already-summarized pattern again, producing nested text like `search "search \"…\" in …" in .`.

**Fix.** Reject unsafe patterns (already a summary, backticks, newlines, overlong) and fall back to `search text`.

**Result.** Closed as a duplicate after maintainer [PR #114933](https://github.com/openclaw/openclaw/pull/114933) landed the same class of fix. Peter (steipete) left a short reply thanking the overlapping contributors and superseding several PRs, including mine. The bug was fixed on `main`; my PR was not the merge vehicle.

### 2) Settings search missing Appearance controls — [#114981](https://github.com/openclaw/openclaw/issues/114981) / [PR #115068](https://github.com/openclaw/openclaw/pull/115068)

**Bug.** Queries like `session observer` / `camera` / `dictation` / `message width` returned nothing, even though the controls already existed under Appearance.

**Fix.** Index those sidebar/chat preference keywords in the settings-search catalog and deep-link to existing anchors. I also posted a small unmocked runtime proof script for ClawSweeper.

**Result.** The issue was closed via a broader maintainer PR ([#115110](https://github.com/openclaw/openclaw/pull/115110)). My branch was behind and conflicted; I closed [#115068](https://github.com/openclaw/openclaw/pull/115068) myself as superseded.

### 3) MCP pin button not refreshing — [#114979](https://github.com/openclaw/openclaw/issues/114979) / [PR #115113](https://github.com/openclaw/openclaw/pull/115113)

**Bug.** Chat thread reactive deps included `canPinWidgets` but omitted `canPinMcpApps`, so the pin control could stay stale when capability flipped.

**Fix.** One-line dependency fix plus a focused UI test.

**Result.** Same wave as above — scooped by [#115110](https://github.com/openclaw/openclaw/pull/115110). I closed the PR.

**Pattern so far:** small UI/display fixes were easy to *do*, hard to *own*, because maintainers were also batching related Control UI work.

### 4) Dashboard `tools.exec` inheritance — [#112376](https://github.com/openclaw/openclaw/issues/112376) / [PR #116244](https://github.com/openclaw/openclaw/pull/116244)

**Bug.** New Dashboard / WebChat sessions could initialize `exec` as `security=deny` instead of inheriting configured `tools.exec` policy.

**Why I walked away.** Review findings kept expanding across CLI loopback grants, Gateway caches, and moving `main`. It stopped looking like a first-contribution-sized change. I closed the PR and said so publicly, then looked for something smaller.

### 5) Quoted prose vs balanced JSON — [#122353](https://github.com/openclaw/openclaw/issues/122353) / [PR #123587](https://github.com/openclaw/openclaw/pull/123587)

**Bug.** `extractBalancedJsonPrefix` selected `{`/`[` *before* tracking quotes, so a brace inside leading quoted prose (e.g. `"notjson{here}"`) became a fake fragment and hid the later real object.

**Fix direction.** Quote-aware start scan in `packages/normalization-core`. That part was straightforward. The hard part was the **adjacent malformed-quote contract**:

- completed quoted spans must stay skipped (the reported bug);
- unterminated quotes still want recovery on today’s `main` (legacy quote-blind behavior);
- some inputs are byte-for-byte ambiguous between those goals.

ClawSweeper walked me through several incorrect intermediate heuristics (whole-input fallback, checkpoint backtracking, `JSON.parse` gates). The version I left documented was the **quote-safe** rule ClawSweeper itself recommended: never re-enter a completed quoted span; accept `null` when malformed quoting makes recovery ambiguous.

![ClawSweeper score history on PR #123587](/assets/img/posts/openclaw-123587-rating-timeline.svg)

Proof and findings landed in a good place (`findings: none`, live direct-function output in the PR body). Merge readiness still bounced between **gold shrimp** and **platinum hermit** because the remaining gate was **maintainer product decision**, not missing tests.

**Parallel path.** A competing CLI-only approach ([PR #122373](https://github.com/openclaw/openclaw/pull/122373)) landed later: restore quote-aware scanning for CLI mixed output, leave the shared helper’s other callers alone. That is a coherent choice; it is just not the shared-extractor contract my PR asked for.

On 2026-09-08 I closed [#123587](https://github.com/openclaw/openclaw/pull/123587). The branch was also conflicted with a later `main` refactor, and sitting open mostly generated review-bot noise.

---

## What the wait taught me

**Silence usually means queue pressure, not a personal snub.** OpenClaw merges a huge volume of PRs. Maintainers were not idle; they were clearing work that can land without a product debate. A P2 that needs an explicit compatibility decision simply sits further back than a patch ClawSweeper can send through on its own.

**“Ready for maintainer look” ≠ “about to merge.”** For [#123587](https://github.com/openclaw/openclaw/pull/123587), that label meant *author-side blockers cleared*. The bot still correctly refused to treat a silent semantic change as done.

**Racing maintainers on UI chores is a bad bet.** Attempts 1–3 were correct patches that lost ownership races. Attempts 4–5 were strategically different: one too large, one product-gated.

**AI can write the patch; proof still has to be visible.** My agent drafted code and tests. Exact-head unmocked outputs and green consumer shards were still what ClawSweeper treated as evidence. Without those, the review stalls regardless of who typed the diff.

**Fork Actions will email you forever.** Upstream schedules (Live/E2E, Stale, PR CI Sweeper) fail on a fork that lacks App secrets. I eventually disabled Actions on the fork entirely after closing the last PR.

---

## Closing note

I still like OpenClaw as an architecture to study. I did not become a merge-listed contributor this round. That is fine. Peter’s short reply on the first PR was a useful reminder that someone had actually looked at the work, even when another commit closed the bug.

If you are aiming at a similar high-velocity repo: pick bugs that are **owned by one helper**, **reproducible without special hardware**, and **not labeled as waiting on a product decision**. And if two strategies exist (shared vs consumer-local), say so early — or you may do the harder correct work and still watch the narrower patch merge first.

Links for the trail:

- [#114484](https://github.com/openclaw/openclaw/pull/114484) · [#115068](https://github.com/openclaw/openclaw/pull/115068) · [#115113](https://github.com/openclaw/openclaw/pull/115113) · [#116244](https://github.com/openclaw/openclaw/pull/116244) · [#123587](https://github.com/openclaw/openclaw/pull/123587)
- Issues: [#113401](https://github.com/openclaw/openclaw/issues/113401) · [#114981](https://github.com/openclaw/openclaw/issues/114981) · [#114979](https://github.com/openclaw/openclaw/issues/114979) · [#112376](https://github.com/openclaw/openclaw/issues/112376) · [#122353](https://github.com/openclaw/openclaw/issues/122353)
