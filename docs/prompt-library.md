# Prompt library — canonical home of P0–P7

Every AI workflow in this repo lives here, full text + operating instructions. The plan references these by number; **this file is the canonical copy** — if a prompt in the plan ever differs from here, this file wins.

Works in Claude, GPT, or GLM. Rule of thumb: Claude for drafting voice, GPT for variations at scale, GLM as overflow.

## How to use any prompt properly (read once)

1. **Copy the block verbatim**, then replace every `[bracket]` with your real data. Brackets are the only parts you edit.
2. **One prompt per chat.** Don't chain P2→P3 in one conversation — context bleeds and the template extraction gets polluted. Exception: paste P3's analysis output into P4 (P4 explicitly asks for it).
3. **Feed real numbers, never vibes.** Anywhere a prompt asks for views/median/tags, paste Sheet values. "It did well" produces generic output; "4.200 vs 900 median" produces analysis.
4. **Never paste secrets.** Tags, post texts, and dashboard numbers are fine. Bank details, KTP/NPWP, passwords — never, in any prompt, ever.
5. **AI drafts, you decide.** Every output ends with your judgment call (schedule / rewrite / discard). The prompts are explicit about forcing that decision.

## Map — which prompt, when

| # | Name | Trigger | Cadence |
|---|---|---|---|
| P0 | Niche validation | Starting, or opening a second account | Once per niche |
| P1 | Pain-point + idea bank | Niche chosen; bank runs dry | Once + monthly refresh |
| P2 | Weekly batch | Every batch day | Weekly |
| P3 | Format lock-in ⭐ | A post does >3x your median views | On event |
| P4 | Repurpose winner | You hold a P3 analysis | On event, winners only |
| P5 | Monthly review | Month-end numbers copied | Monthly |
| P6 | Flop autopsy | 5+ dead posts, or monthly alongside P5 | On event / monthly |
| P7 | Reply drafts | Daily engagement (warm-up + ongoing) | Daily, 10 min |

---

## P0 — Niche validation

**WHEN:** before committing to a niche (including lane #2). Companions: [choose-your-niche](choose-your-niche.md).

**INPUTS (you supply):** 2–3 candidate niches + your constraints (faceless? hours/week?).

**PROMPT:**
```
I run faceless social accounts in Indonesia (no face, no voice, text + hands-only visuals) to promote Shopee affiliate products via useful content. I have [3–5] hours/week.
Candidate niches: [1. small-space home living / kos-kosan hacks; 2. beauty/skincare basics; 3. budget phone accessories].
Task: (1) Score each against these 5 criteria — faceless-native, impulse price band Rp20–150rb, obvious Shopee search keywords, carousel-friendly, low claim/regulatory risk. Table format with 1-line evidence per cell. (2) For the top scorer, list 10 audience pain points in their own words + 1 Shopee search keyword each. (3) Give a go/no-go verdict with the single biggest risk of the winner.
Constraints: Bahasa Indonesia examples; no medical/efficacy claims anywhere.
```

**OUTPUT:** scored table + 10 pains with keywords + verdict + top risk.

**INTERPRET:** go only if the winner passes all 5 criteria AND you can add 5 more pains from memory (proves you know the audience). The 10 pains become P1's seed input. If no candidate passes → niche down (e.g. "beauty" → "kos-kosan cleaning") and re-run. Next: P1.

---

## P1 — Pain-point + idea bank

**WHEN:** niche chosen; refresh monthly or when P2 starts repeating itself.

**INPUTS:** niche name + audience sketch (who, budget, where they shop).

**PROMPT:**
```
Context: I run a faceless Threads/X account in Indonesia, niche: [small-space home living / kos-kosan organization & cleaning hacks]. Audience: [anak kos + young families, budget-conscious, shops on Shopee]. Posts are plain text, no sales pitch, link only in comments.
Task: (1) List 15 specific pain points this audience complains about in their own words. (2) For each, give 2 post angles (story/relatable + practical list). (3) Output as a table: Pain | Angle A | Angle B | Shopee search keyword to find a matching product.
Constraints: everyday Bahasa Indonesia, no medical/claim language, no product I must claim to have personally tested. Ideas must be filmable later as text-only, carousel, or hands-only video.
```

**OUTPUT:** 15-row bank table (30 angles + keywords).

**INTERPRET:** save the whole table to your notes/Sheet — this is the fuel P2 draws from for weeks. Quality bar: every row must name a concrete object or situation ("kabel berantakan di kos"), never a vague topic ("tips kerapian"). Vague rows → ask a follow-up ("give 3 concrete sub-situations for row 7") before accepting. Next: P2 weekly.

---

## P2 — Weekly batch ideation (10–14 posts)

**WHEN:** every batch day. Companions: [content-examples](content-examples.md) for the voice reference.

**INPUTS:** P1 bank (or, once data exists, your 2–3 best posts + their views).

**PROMPT:**
```
Context: [paste your 2–3 best past posts + views, or say "new account, no data yet, use P1 bank"].
Niche: [small-space home living]. Voice reference: [paste 1 post you like from docs/content-examples.md].
Task: Write 12 Threads posts, each under 400 characters, Bahasa Indonesia casual. Mix: 4 relatable stories, 4 practical lists/tips, 4 "mistake I see people make" posts. Each ends with a soft loop (question or "part 2?") but NO link, NO CTA to buy, NO "link di komen".
For each post add: (a) suggested Shopee search keyword for the comment link, (b) 1-line first-comment text to accompany the link later.
```

**OUTPUT:** 12 posts + per-post keyword + first-comment line.

**INTERPRET:** accept rate should be ~8/12 usable — discard anything that sounds like an ad, exceeds 400 chars, or needs a claim you can't support. Build one tagged link per accepted post, queue 2/day, log every row in `posts`. The (a)/(b) lines are what make check-ins 10-minute work instead of 40. Next: schedule → check-ins → P3 on any outlier.

---

## P3 — Format lock-in: reverse-engineer a winner, clone x10 ⭐

**WHEN:** one post beats your median views >3x. This is the money workflow — everything else feeds it winners.

**INPUTS:** winner text (exact), its views [N], your current median [M], plus 5–10 fresh topics from the P1 bank.

**PROMPT:**
```
This post outperformed (views: [N], median: [M]): "[paste winning post text]".
Task: (1) Reverse-engineer WHY it worked: hook pattern (first 15 words), structure (lines, breaks, list vs story), emotional trigger, specificity, open loop. Be concrete, quote the mechanism. (2) Extract the abstract template in 3–5 slots, e.g. HOOK + RELATABLE SETUP + 3 ITEMS + LOOP. (3) Write 10 NEW posts in the SAME template but DIFFERENT topics from my idea bank (no repetition). Each under 400 chars, Bahasa Indonesia, no link in body. (4) For each: 1-line first-comment text + Shopee search keyword.
Constraint: do not change the template's rhythm. Same line breaks, same length band, same POV.
```

**OUTPUT:** mechanism analysis + named template + 10 clones with comment lines.

**INTERPRET:** check part (1) first — if the "mechanism" is generic ("good hook, relatable"), push back once ("quote the exact words doing the work") before accepting the clones. Good clones feel like siblings, not paraphrases: same rhythm, new topics. Schedule the 10 across ~2 weeks (don't dump in 2 days), one template at a time — running two P3 templates simultaneously destroys attribution. Save the analysis text: P4 needs it verbatim. Next: P4 for this winner.

---

## P4 — Repurpose winner to carousel + faceless video

**WHEN:** you hold a P3 analysis. Winners only — never spend Canva/CapCut hours on unproven posts.

**INPUTS:** winner text + the P3 analysis output (paste both).

**PROMPT:**
```
Winner post: "[paste]". Proven hook: "[paste P3 analysis]".
Task A (IG carousel, 7 slides): Slide 1 = hook (max 8 words, curiosity, same promise as winner). Slides 2–6 = one idea per slide, max 18 words each, plain words. Slide 7 = soft closer + "detail contohnya aku taruh di komen/bio". Provide Canva-ready text per slide + visual note (hands-only / room photo / icon; no face, no voice).
Task B (TikTok/Reels, 20–30s, fully faceless, NO voiceover): 6–8 shots, each with on-screen text (max 6 words) + shot description (close-up hands, before/after, screen record of Shopee listing). Suggest pacing (cuts every 3s) + caption + hashtag set (5 niche + 2 broad ID). No spoken lines, trending instrumental audio assumed.
Same hook, same structure, new format. Do not invent claims ("terbukti", "aku pakai 2 tahun") unless I confirm.
```

**OUTPUT:** 7 slide texts + visual notes; 6–8 shot list + caption + hashtags.

**INTERPRET:** build in Canva free (one reusable 7-slide template) + CapCut (text overlay, trending instrumental). ~1 hr per winner total. Log as `car`/`vid` rows sharing the winner's serial root (e.g. winner `t008` → `t008_car`, `t008_vid`) so the pivot can compare formats. If a slide needs a premium Canva asset → swap the visual, never pay. Reference output: [content-examples](content-examples.md#carousel-version).

---

## P5 — Monthly performance review (strict numbers)

**WHEN:** month-end, dashboard numbers copied. First-timer? Do the [fictional walkthrough](monthly-review-example.md) first.

**INPUTS:** (a) `posts` rows for the month (post_id, platform, format, template, tag, views/likes/replies); (b) dashboard copy per tag (Klik, Pesanan, Produk Terjual, Pesanan Rp, Komisi Kotor Rp, status mix); (c) the month + how much commission is still pending.

**PROMPT:**
```
You are my performance analyst. DATA FOLLOWS. Use ONLY the real numbers below — never estimate, never invent, never round into claims. If a field is missing, say "missing" and exclude it from that calculation.
[Paste (a), (b), (c).]
Task: (1) Join on tag. Report per platform×format×template: posts, clicks, orders, GMV, commission (split approved vs pending), EPC, click-through proxy (clicks/views where views exist). (2) Flag winners (>3x median views AND top-quartile EPC) vs volume traps (high views, ~0 commission) vs dead (bottom-quartile both). (3) Recommend START (double down with P3+P4), CONTINUE (hold volume), STOP (pause this template/platform for 30 days) — one line each with the number that justifies it. (4) List exactly what to do next week (max 5 actions). End with: "Assumptions I did NOT make:" + open data gaps.
Constraints: modest side-income framing; no get-rich claims; no advice that violates platform spam rules or requires false testimonials.
```

**OUTPUT:** join table + winner/trap/dead flags + START/CONTINUE/STOP lines + 5 next actions + assumptions list.

**INTERPRET:** apply the verdicts literally for 30 days: winner → P3+P4; trap → same format, one new product category; dead → slots reallocated. Read the assumptions list every time — if it says "assumed pending converts at 100%", discount the EPC yourself. Pending is not cash; GMV is never earnings. See the [worked example](monthly-review-example.md) for what correct output looks like.

---

## P6 — Flop autopsy (the inverse of P3)

**WHEN:** 5+ posts sit in the bottom quartile, or monthly alongside P5. Never rewrite more than the flops — winners get clones, flops get lessons.

**INPUTS:** 3–5 dead posts (exact texts + views each) + your median + the template each was supposed to follow (if any).

**PROMPT:**
```
These posts flopped (median views: [M]): [paste each with its views: T011 120 views, T012 95 views, ...]. Intended templates: [T011 list3, T012 story, ...]. Niche: [small-space home living].
Task: (1) Diagnose EACH post separately: hook failure (first 15 words give no reason to read on?), structure failure (wall of text? no breaks?), topic failure (no buying intent? too generic?), mismatch (post promises X, comment link sells Y?). Quote the failing words. (2) Give 1 rewrite per post fixing ONLY the diagnosed fault — same topic, same template, under 400 chars, Bahasa Indonesia, no link in body. (3) End with the shared pattern across all flops in one sentence (e.g. "all hooks lack a number or size").
Constraint: do not turn flops into a different template. Fix, don't redesign.
```

**OUTPUT:** per-post diagnosis with quoted faults + 1 rewrite each + one-sentence shared pattern.

**INTERPRET:** test at most 1 rewrite per flop (schedule like normal posts, fresh tags). The real prize is part (3): if every flop lacks specifics, the fault is in your P2 instructions — append one line to future P2 runs ("every post must contain one number, size, or price") instead of nursing individual posts. If flops share no pattern, it's variance, not skill — post more, diagnose less.

---

## P7 — Reply drafts (daily engagement, 10 min)

**WHEN:** daily during warm-up; 2x/week ongoing. Replies are half the algorithm game for a faceless account — this keeps them in-voice without thinking.

**INPUTS:** the post/comment you're replying to (paste exact text) + thread context in one line.

**PROMPT:**
```
Context: someone else's post in my niche ([small-space home living]): "[paste their post text]". My account voice: [helpful anak-kos senior, casual Bahasa Indonesia, never salesy].
Task: draft 3 reply options, each under 200 characters: (1) value-add (one concrete tip extending their point), (2) question (opens a thread), (3) relatable (short shared experience, no product mention).
Constraints: NO links, NO product names, NO "cek tokoku", NO emojis spam (max 1). Must read like a real person, not a brand.
```

**OUTPUT:** 3 reply options.

**INTERPRET:** post exactly ONE (best fit), lightly humanized — never all three, never verbatim every time. Skip replies on controversial/political/giveaway-bait threads no matter how tempting the reach. During warm-up this is your main activity (5–10/day); afterwards it shrinks to check-in duty (Appendix B).
