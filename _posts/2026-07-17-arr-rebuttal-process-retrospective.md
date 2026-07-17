---
title: "From Skipping Rebuttal to Raising a Score: An ARR Process Retrospective"
date: 2026-07-17 10:30:00 +08:00
categories:
  - research
tags:
  - arr
  - rebuttal
  - tool-learning
  - academic-writing
  - workflow
toc: false
---

In 2026 I submitted the same tool-learning project to **two ACL ARR cycles** — March, then May. Reviews arrive about two months after submission, so the rebuttal work for the May cycle landed in July. The first cycle ended poorly enough that we skipped rebuttal and rebuilt the paper. The second cycle went much better — and a careful rebuttal moved one reviewer's score up.

This post is a **process retrospective**: what the reviews looked like at a high level, how we decided when *not* to rebuttal, and how I actually wrote the second-round responses.
---

## Round 1 (ARR 2026 March): 3 / 2 / 1.5

Initial overall assessments were **3, 2, and 1.5**. The 1.5 came with **confidence 5** — the reviewer had read carefully and was not guessing. The area chair's meta-review pointed the same direction: the paper needed **substantial revisions** before the next cycle.
Across reviewers and the meta-review, the recurring themes were:

- **Data distribution / imbalance** — training and evaluation were dominated by a few sources; aggregate metrics could be misleading
- **Synthetic-data novelty and impact** — unclear how our synthesis differed from prior pipelines, and the synthetic subset was tiny relative to public data, with weak ablations
- **Missing comparisons and details** — limited comparison to existing multi-turn synthesis work; insufficient implementation detail for reproducibility
- **Evaluation design** — fixed candidate-tool settings, shallow multi-turn evaluation relative to execution-based benchmarks, and readability / presentation issues

At that point, a short rebuttal window would not have fixed the core problems. So we **did not rebuttal**. Instead we treated the reviews as a revision checklist: rebalance evaluation, strengthen synthesis claims with evidence, expand experiments and analysis, and clean up the writing. Almost everything the reviewers asked for went into the next manuscript.

---

## Round 2 (ARR 2026 May): 3 / 2.5 / 2.5 → one raise to 3

After the overhaul, the new reviews were **3, 2.5, and 2.5**. The tone was different. Reviewers still pushed on important points — **model scale**, **data-processing / conversion details**, **deeper analysis of failure modes** (especially multi-turn), and **positioning vs related work** — but the asks were concrete and mostly answerable inside the rebuttal period.
We wrote detailed per-reviewer responses, added small follow-up experiments (including scaling within and beyond the original backbone family), and clarified several protocol details with tables. One of the **2.5** reviewers later wrote that the clarifications addressed key concerns and **raised the score to 3**. No other score changed after that.

The rebuttal discussion period is now over. We are waiting for the **AC decision around late July / early August**.

---

## The Workflow That Actually Worked

One line summary: **Gemini for strategy, Cursor for drafting the response text.**

More precisely:

1. **Strategy first (Gemini in AI Studio).** I am on Gemini Pro. Before touching OpenReview prose, I asked Gemini for a revision / rebuttal plan: which concerns are decision-critical, what evidence we already have, what small experiments are worth running, and how to structure replies without sounding defensive.
2. **Meeting with co-authors.** I brought that plan to a co-author meeting. They challenged priorities, suggested better framings, and pointed out claims that needed softening or stronger evidence.
3. **Draft in Cursor.** After the meeting, I wrote the actual responses in Cursor. For this kind of long, structured academic writing with many tables and cross-references, the editor workflow was far more convenient than drafting only in a browser box.
4. **Advisor pass.** I sent the draft to my advisor. The feedback improved both tone and substance — including a request for **additional experiments** beyond what was already in the first batch of replies.
5. **Archive everything in Google Docs.** Every draft version, table, and timeline lived in Docs so co-authors could comment and so I could reconstruct what was submitted when.

---
## Staged Submission During the Rebuttal Window

We did **not** dump everything on the last day. Rough timeline:

| When | What we posted |
|------|----------------|
| ~4 days before the deadline | Main per-reviewer responses — already including experiments and analysis tables |
| ~2 days before | Extra experiments requested after the advisor meeting (e.g., more scaling / cross-family checks) |
| Last day | A short **general response** |

The general response had two jobs:

1. **Help the AC** — a one-screen map of what we answered (scaling, conversion details, multi-turn analysis, related-work positioning), with pointers to the individual threads
2. **Prompt reviewer replies** — give reviewers a clear reason to come back to the discussion and respond to our rebuttal, not leave the thread silent after we posted

Per-reviewer comments alone are easy to overlook in a busy inbox. A short general response makes the ask visible: we answered your points — please take another look.

---
## Tone Template: Thank First, Then Answer Point by Point

Almost every reply followed the same shape:

1. Thank the reviewer and **echo one specific strength they mentioned** (not empty flattery)
2. Restate each weakness / suggestion in their language
3. Answer with **evidence** (table, ablation, clarification, or a precise camera-ready promise)
4. Close politely without begging for a score

A reusable skeleton (paraphrased, not a real paste):

> We thank the reviewer for the careful and constructive comments. We appreciate your recognition of \[specific strength\]. We address each point below.
>
> **W1: \[restated concern\].** \[Evidence / clarification / new result\]. We will \[concrete camera-ready change\] if needed.
>
> **W2: …**

That opening matters. Reviewers are more willing to re-read when they feel heard on what they already liked.

---

## What I Would Repeat

- **Skipping rebuttal can be the right call** when the paper needs a rebuild, not a paragraph
- **Treat harsh high-confidence reviews as a gift checklist**, then actually execute it before the next cycle
- **Separate strategy from prose**: plan with a strong model, draft in an editor that can hold long structured replies
- **Ship in stages**: early substantive replies, then new experiments, then a general response that helps the AC and invites reviewers to reply- **Lead with thanks for concrete positives**, then answer with evidence

I do not know yet whether the second-cycle paper will be accepted. What I do know is that the rebuttal process itself felt much more under control this time — less panic, more project management.

If you are staring at a mixed ARR stack and wondering whether to fight this cycle or rebuild for the next one, I hope this retrospective makes the trade-off a little clearer.
