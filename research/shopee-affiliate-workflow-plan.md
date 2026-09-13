# Shopee Affiliate Organic Growth — End-to-End Workflow Plan
Date: 2026-09-13
Status: Ready to execute today
Assumed operator profile: starting from zero on Shopee Affiliate, ~3–5 hrs/week alongside a day job, fully faceless (no face, no voice). Niche default: small-space home living / kos-kosan (re-decide via docs/choose-your-niche.md). Tracking default: Google Sheets (see tracking/ + §5). Adapt the profile to yours — the system holds as long as the cadence does.
Operative reference: playbook summary in brief (X thread background only). Free-tier limits change fast — validate each at signup; links below are plain (no referrals).

> Senior-growth-engineer verdict up front: do NOT build anything custom. A single Google Sheet + Shopee's own tagged links + a free scheduler covers 100% of what you need until you are doing >200 posts/month or running 3+ accounts. Custom Postgres is not justified at your scale. Details in §5.

---

## 0. How this system works (the 30-second model)

1. You post useful, niche content (no sales pitch). Link lives ONLY in first comment/reply.
2. Every link is a Shopee-tagged custom link: `platform_account_content`.
3. Clicks open a 7-day window: anything the clicker buys on Shopee in 7 days earns you commission (indirect sales). Per playbook — treat product choice as incidental, click volume as the lever. Verify current cookie/commission rules inside your own Affiliate dashboard on day one (Shopee changes rates by category and campaign period).
4. Volume finds winners (~0.5% hit rate is the working model = ~1 in 200 posts pops). AI clones the winning *format* (hook/structure/emotion), not the topic. Winners get repurposed to carousel + faceless video because IG/TikTok have long-tail shelf life.
5. Monthly: copy Shopee dashboard numbers → strict-numbers AI review → start/stop/continue. (No CSV export exists — manual copy, ~10 min.)

With 3–5 hrs/week you cannot post 5x/day manually. You batch once, schedule, then check in every few days for replies + stats. That is the whole design constraint below.

---

## 1. Account / platform setup checklist (Phase 0 — do once, ~2 hrs)

### 1.1 Shopee Affiliate (your own account, no referrals)
- [ ] Register at Shopee Affiliate Indonesia under your own Shopee account (app: Saya > Shopee Affiliates Program, or affiliate.shopee.co.id). Complete tax/bank/payout info. Note payout threshold + schedule shown in YOUR dashboard — do not trust screenshots from others.
- [ ] Learn two screens on day one: (a) Custom link builder (where you paste a Shopee product URL and add tags — look for the "Pakai Tag: Ya" toggle), (b) Reports: `Laporan Performa` (Klik / Pesanan / Produk Terjual / Pesanan Rp / Komisi Kotor Rp) + `Laporan Klik` per tag. If either screen is missing, your account tier is not fully approved — stop and finish verification before posting.
- [ ] Decide tag taxonomy NOW and never deviate. Format: lowercase, no spaces, max 3–4 segments:
  - `platform`: `th` (Threads), `x`, `ig`, `tt`, `fb`
  - `account`: e.g. `a1` (if you later add a second account, `a2`)
  - `content`: serial + format, e.g. `t042_txt`, `t042_car`, `t042_vid`
  - Full example: `th_a1_t042_txt`. Rule: every link gets all 3. One post = one tagged link (never reuse the same tag on two posts or attribution dies).
- [ ] Pick 5–10 evergreen Shopee products in your niche to link first (see §2 for niche). Criteria: rating 4.8+, sold 10k+, price Rp20–150rb (impulse range, high click-to-checkout), non-regulated (no skincare medical claims, no supplements). You will rotate these; the specific product matters less than volume.

### 1.2 Social accounts (faceless)
- [ ] Threads (primary door): 1 fresh account, niche name (not your real name), plain avatar (icon/pattern), bio = who this helps + posting promise, NO link in bio yet (add link-in-bio only after 30 posts to look native, not spammy).
- [ ] X (secondary, same content, zero extra ideation): same handle if available, same bio.
- [ ] IG + TikTok (repurposing only, Phase 4): same handle, switch to Creator/Business (free analytics), bio link = single link-in-bio page (see §4).
- [ ] Warm-up (days 1–7): no links at all. Post 1–2 value posts/day, reply 5–10x/day in-niche. Goal is to look like a real person to the algorithm before you ever drop a link. New accounts that post links on day one get throttled — this is the most common beginner kill.

### 1.3 Scheduler + tracker + link-in-bio (all free tier, validate at signup)
- [ ] Scheduler: start with Buffer free (simplest) — connect Threads + X first. Verify current free limits inside the app before you commit (historically ~3 channels + ~10 queued posts per channel; limits change). If Buffer free no longer covers Threads, fallback order: Publer free → Metricool free (Later has no free plan — trial only, skip it). Pick ONE; do not multi-tool.
- [ ] Tracker: one Google Sheet (see §5). Create it now, before your first linked post.
- [ ] Link-in-bio (only for IG/TikTok phase): one Beacons free page (or Linktree free). One page, max 5 links. You do not need a custom domain.

---

## 2. Content workflow — niche, format lock-in, repurposing

### 2.1 Niche recommendation (default — re-decide for yourself)
Assumed profile for this default: faceless-only beginner with no strong niche preference.
> Re-deciding for someone else (or your second account)? Use the framework, not the answer: `../docs/choose-your-niche.md`.

Recommendation: **start with small-space home living / kos-kosan + cleaning-organization hacks** (sub-slice of gadgets/home living). Why:
- Faceless-native (photos of rooms, hands-only demos, text lists — no face or skin trust needed). Beauty/skincare as a faceless beginner is high-friction: trust + skin-type claims + BPOM/claim risk + brutal competition.
- Endless Shopee-mapped pain points (storage, dapur sempit, kamar kos, kabel berantakan) in the Rp20–150rb impulse band.
- Carousel-friendly (before/after, checklist, "5 barang under 50rb") and faceless-video-friendly (hands + text overlay + trending audio, no voice needed).
- Keep beauty as expansion lane #2 only after you have one winning text format — do not run two niches at once at 3–5 hrs/week.

Voice rule: genuinely useful or relatable, Bahasa Indonesia casual, never a sales pitch in the post body. No "aku sudah coba" unless you actually bought it. Compliant alternative: "yang ratingnya paling stabil di kategori ini…" / "komentar pembeli banyak bilang…".

### 2.2 Operating cadence (3–5 hrs/week)
- **Batch day (1x/week, ~2 hrs):** generate 10–14 text posts with AI (templates below), build Shopee tagged links (one per post), queue in Buffer (2/day Threads + mirror to X). Log every post in Sheet (30 sec each).
- **Check-ins (2x/week, 20–30 min each):** post the scheduled first-comment link promptly if your scheduler cannot auto-post first comments; reply to comments; record views/likes/replies; note any outlier (>3x median views = candidate winner).
- **Monthly (1 hr):** copy Shopee dashboard numbers → run review prompt (§6) → decide start/stop/continue.

Volume math (honest): at 2/day you do ~56 text posts/month. At a 0.5% hit model that is ~0.3 hits/month early on — i.e., expect 2–3 months to find your first proven format. This is a consistency asset, not monthly salary. If after 150 posts you have zero outliers, the niche or hook family is wrong — change one variable, not everything.

### 2.3 Link placement rule (non-negotiable)
- Post body: NEVER contains a URL. Platforms suppress outbound-link posts.
- First comment/reply (your own account, within 15–60 min of posting): 1 line context + tagged link. Example: "yang aku maksud yang model gini btw: [tagged link]". One link per post. No link-stuffing, no DM spam, no shortening tricks that hide the Shopee domain.

### 2.4 Ready-to-paste AI prompt templates (works in Claude / GPT / GLM)

**P1 — Pain-point + idea bank (run once per niche, then monthly refresh)**
```
Context: I run a faceless Threads/X account in Indonesia, niche: small-space home living / kos-kosan organization & cleaning hacks. Audience: anak kos + young families, budget-conscious, shops on Shopee. Posts are plain text, no sales pitch, link only in comments.
Task: (1) List 15 specific pain points this audience complains about in their own words. (2) For each, give 2 post angles (story/relatable + practical list). (3) Output as a table: Pain | Angle A | Angle B | Shopee search keyword to find a matching product.
Constraints: everyday Bahasa Indonesia, no medical/claim language, no product I must claim to have personally tested. Ideas must be filmable later as text-only, carousel, or hands-only video.
```

**P2 — Weekly batch ideation (10–14 posts)**
```
Context: [paste your 2–3 best past posts + views, or say "new account, no data yet, use P1 bank"].
Task: Write 12 Threads posts, each under 400 characters, Bahasa Indonesia casual. Mix: 4 relatable stories, 4 practical lists/tips, 4 "mistake I see people make" posts. Each ends with a soft loop (question or "part 2?") but NO link, NO CTA to buy, NO "link di komen".
For each post add: (a) suggested Shopee search keyword for the comment link, (b) 1-line first-comment text to accompany the link later.
```

**P3 — Format lock-in: reverse-engineer a winner, clone x10 (THE key workflow — run only when a post does >3x your median views)**
```
This post outperformed (views: [N], median: [M]): "[paste winning post text]".
Task: (1) Reverse-engineer WHY it worked: hook pattern (first 15 words), structure (lines, breaks, list vs story), emotional trigger, specificity, open loop. Be concrete, quote the mechanism. (2) Extract the abstract template in 3–5 slots, e.g. HOOK + RELATABLE SETUP + 3 ITEMS + LOOP. (3) Write 10 NEW posts in the SAME template but DIFFERENT topics from my idea bank (no repetition). Each under 400 chars, Bahasa Indonesia, no link in body. (4) For each: 1-line first-comment text + Shopee search keyword.
Constraint: do not change the template's rhythm. Same line breaks, same length band, same POV.
```

**P4 — Repurpose winner to carousel + faceless video (run only for proven winners)**
```
Winner post: "[paste]". Proven hook: "[paste P3 analysis]".
Task A (IG carousel, 7 slides): Slide 1 = hook (max 8 words, curiosity, same promise as winner). Slides 2–6 = one idea per slide, max 18 words each, plain words. Slide 7 = soft closer + "detail contohnya aku taruh di komen/bio". Provide Canva-ready text per slide + visual note (hands-only / room photo / icon; no face, no voice).
Task B (TikTok/Reels, 20–30s, fully faceless, NO voiceover): 6–8 shots, each with on-screen text (max 6 words) + shot description (close-up hands, before/after, screen record of Shopee listing). Suggest pacing (cuts every 3s) + caption + hashtag set (5 niche + 2 broad ID). No spoken lines, trending instrumental audio assumed.
Same hook, same structure, new format. Do not invent claims ("terbukti", "aku pakai 2 tahun") unless I confirm.
```

**P5 — Monthly performance review (strict numbers — see §6 for full version)**
Short form pasted here so you have it with the others; full rules in §6.

---

## 3. Scheduling / publishing

Recommended: **Buffer free** to start. Why it wins for this profile: fastest Threads+X queue setup, simplest UI for a beginner, enough for 2/day batching at this volume. Connect Threads + X only in Phase 1; add IG + TikTok in Phase 4. House rule: sign up directly at buffer.com under your own account — do NOT use referral shortlinks (including the `s.id/joinbuffer` link from the source thread). Every tool account is created fresh under your own name, no exceptions.

Note on the source thread's other two links: (1) the "Threads-to-Carousel skill" Tally form is the creator's own lead-magnet form — skip it; prompt P4 in §2.4 already covers that repurposing workflow inside any capable LLM, with no data handed to a third party. (2) The "ChatGPT Go gratis 3 bulan" Shopee promo is redundant if you already hold a paid ChatGPT subscription (which outranks Go); otherwise ignore it — nothing in this workflow needs it.

Fallback order if Buffer free limits bite (validate inside each app, limits change quarterly): Publer free (3 accounts, 10 pending/account) → Metricool free (20 posts/mo total — tight, analytics fallback only). Later has no free plan (14-day trial only) — skip. Do not pay for any scheduler until one format is proven AND you are exceeding the free queue more than twice a month — that is the only upgrade trigger.

Practical notes:
- Schedulers sometimes cannot auto-post the *first comment* on Threads/X. Assume YOU post the first-comment link manually during check-ins. This is why check-ins exist.
- Keep a 2-day rolling queue minimum so a missed day does not break consistency.
- Never schedule >3/day/account in month one (new-account velocity flag).

---

## 4. Tool comparison table (free tiers — VALIDATE at signup, Sept 2026)

| Need | Pick | Free tier (verify in-app; changes often) | Why this over alternatives |
|---|---|---|---|
| Text scheduling (Threads+X) | Buffer free | Historically ~3 channels, ~10 queued/channel. Confirm now. | Simplest queue; Threads support mature. Publer free is the fallback; Metricool free (20/mo) is analytics-fallback only. Later has no free plan — skip. |
| Analytics fallback | Metricool free | Historically ~50 posts/mo quota + per-post stats. Confirm now. | Best free analytics if Buffer stats feel thin. Not needed day one. |
| Tracking DB | Google Sheets free | Effectively unlimited for this scale; 10M cells. | Lowest friction, paste-friendly (dashboard numbers are hand-copied), pivot-ready, no record caps that matter. Notion is prettier but slower for joins; Airtable free has record caps that will annoy you by month 4–6. |
| Link-in-bio (IG/TikTok only) | Beacons free (alt: Linktree free) | Free page + basic analytics; custom domain is paid (skip it). | Beacons free gives more blocks (video/async) for faceless video funnel; Linktree free is fine if you prefer simpler. One page, ≤5 links. |
| Carousel design | Canva free | Free templates + exports; some assets Pro-locked (avoid them). | Fastest non-designer path; 7-slide template reusable. Figma is overkill; Adobe Express free is viable alt. |
| Faceless video edit | CapCut free (desktop+mobile) | Free edit/export; check current export/watermark & stock-audio licensing in-app. | Text-overlay + auto-captions + trending sounds fastest for no-voice workflow. VN free is the offline fallback. |
| LLMs | Any capable LLM (Claude / GPT / GLM) | Use what you have. | Drafting voice, variations at scale, overflow/batch. No new AI spend. |

Explicitly NOT recommended now: any paid scheduler, paid link tracker (Bitly paid, etc. — Shopee tags already attribute; extra shorteners add breakage + cost), custom-built tracker, paid domain, paid stock sites.

---

## 5. Tracking solution (no custom build justified)

### Verdict: use Google Sheets. Custom Postgres is NOT justified.
Why existing tools win at your scale (<100 posts/mo, 1 person, Shopee dashboard numbers hand-copied monthly, no API to integrate, no multi-user need):
- Shopee already attributes by tag — you only need to JOIN your post log to Shopee's export on the tag string. That is a VLOOKUP/pivot, not an app.
- Sheets handles 10k rows effortlessly; your year-one volume is ~700 posts. Airtable free record caps and Notion's weak CSV-join ergonomics are worse fits, though both *could* work.
- A custom DB earns its keep only if: 3+ accounts × 10+ posts/day, or you need auto-ingest of Shopee reports via scraping/API (fragile, ToS-sensitive, maintenance burden that kills a side project). Revisit only when manual monthly joins take >1 hr/month AND income covers infra.

### Minimal data model (3 tabs)
**Tab 1 — `posts`** (one row per post, filled at scheduling time, 30 sec/row):
`post_id` (e.g. T042) | `date_posted` | `platform` (th/x/ig/tt) | `account` | `format` (txt/car/vid) | `post_url` | `hook_first15words` | `template` (e.g. list3/story/mistake) | `topic` | `shopee_tag` (exact string, e.g. th_a1_t042_txt) | `shopee_product_url` | `views` | `likes` | `replies` | `notes`

**Tab 2 — `links`** (optional until Phase 4; one row per tagged link if you reuse products):
`shopee_tag` | `product_name` | `product_url` | `price_band` | `category`

**Tab 3 — `performance_import`** (manual copy from Shopee dashboard monthly — no official CSV export documented; never hand-retype tags, copy-paste; add one column):
Shopee `Laporan Performa` columns as-is (`Klik`, `Pesanan`, `Produk Terjual`, `Pesanan (Rp)`, `Komisi Kotor (Rp)`, refreshed daily 16:30 WIB) + `post_id` (VLOOKUP from tag) + `month`. Commission counts only for completed/validated orders; split approved vs pending in the pivot.

**Monthly view:** pivot by `platform × format × template` → clicks, orders, commission, EPC (commission/clicks). EPC per tag is your start/stop/continue input.

Rules: tag strings must match EXACTLY (no retyping — copy-paste from Shopee tool into Sheet). Never edit past `performance_import` rows; append new month as new rows.

---

## 6. Periodic review routine (monthly, 1 hr) + strict-numbers prompt

Cadence: monthly for decisions (Shopee statuses settle slowly: pending→approved), with a 5-min mid-month sanity glance (any outlier → feed to P3 immediately, do not wait).

**P5 — full monthly review prompt (paste with your CSV):**
```
You are my performance analyst. DATA FOLLOWS. Use ONLY the real numbers below — never estimate, never invent, never round into claims. If a field is missing, say "missing" and exclude it from that calculation.
[Paste: (a) posts tab rows for the month (post_id, platform, format, template, tag, views/likes/replies), (b) Shopee export rows (tag, clicks, orders, GMV, commission, status). State the month + status mix (how much is still pending).]
Task: (1) Join on tag. Report per platform×format×template: posts, clicks, orders, GMV, commission (split approved vs pending), EPC, click-through proxy (clicks/views where views exist). (2) Flag winners (>3x median views AND top-quartile EPC) vs volume traps (high views, ~0 commission) vs dead (bottom-quartile both). (3) Recommend START (double down with P3+P4), CONTINUE (hold volume), STOP (pause this template/platform for 30 days) — one line each with the number that justifies it. (4) List exactly what to do next week (max 5 actions). End with: "Assumptions I did NOT make:" + open data gaps.
Constraints: modest side-income framing; no get-rich claims; no advice that violates platform spam rules or requires false testimonials.
```

Decision heuristics (defaults, override with your numbers): winner → 10 clones via P3 + 1 carousel + 1 video via P4; volume trap → keep format for views but swap comment-link product category once before killing; dead 30 days → stop, reallocate that slot to winner's template.
> Never run P5 before? Read the fictional worked example first: `../docs/monthly-review-example.md`. Jargon check: `../docs/glossary.md`.

---

## 7. Tech stack recommendation (CONDITIONAL — only if custom tracking is ever justified)

Not justified now (§5). If you ever outgrow Sheets (multi-account, auto-ingest need, >1 hr/mo manual joins sustained 3 months), build the smallest thing that works:

- **DB: PostgreSQL** (the default if this is ever built: reliable JOINs on tag strings, CSV COPY ingest, free managed tiers).
- **App: Next.js (TypeScript) + Drizzle (or Prisma) + PostgreSQL + shadcn/ui + Tailwind.** Rationale: (a) debuggability — one language end-to-end, Drizzle's typed inspectable SQL (or Prisma Studio) + Next dev overlay + Vercel/Node logs a beginner can read; (b) library richness — migrations + CSV ingest, shadcn/ui + TanStack Table (grids/pivots without building UI), Recharts (EPC views), NextAuth (later); (c) speed — CRUD + CSV upload + pivot page is a weekend scaffold, not a framework project. Hosting: Neon/Supabase Postgres free tier + Vercel free tier for validation; keep Shopee dashboard entry manual (no scraping — ToS/maintenance trap).
- **Schema (if built):** `posts(post_id PK, posted_at, platform, account, format, template, topic, post_url, tag UNIQUE, product_url, views, likes, replies)` + `perf_rows(id PK, tag FK, date, clicks, orders, gmv, commission, status, import_batch)` + view `epc_by_tag`. That is the whole app. Anything bigger is over-engineering.

Do not build this in Phase 0–5. Build it only on the trigger above.

---

## 8. Phased implementation plan (execute in order, no skipping)

**Phase 0 — Setup (this week, ~2–3 hrs):** Shopee registration + payout check; tag convention written down; Threads+X accounts + 7-day warm-up starts; Buffer free connected; Google Sheet created from §5 schema; Beacons page reserved (empty).
*Done when:* you can generate a tagged link and it appears in your Sheet via copy-paste.

**Phase 1 — First content loop, manual (weeks 2–5, 3–5 hrs/week):** run P1 → P2 weekly; 1–2/day Threads + mirror X; links only in first comments; log every post; NO carousel/video yet. Goal is not income — it is finding one template that beats your median 3x.
*Done when:* 60–100 text posts logged OR first winner found.

**Phase 2 — Tracking live (from post #1, 30 sec/post + 1 hr first monthly review):** fill `posts` at schedule time; paste first Shopee export; run P5 once even on thin data to practice the loop.
*Done when:* one pivot table exists joining tags → clicks/commission.

**Phase 3 — AI scaling (starts at first winner):** run P3 → 10 clones → batch-schedule. One template at a time. Kill nothing until 30 days of data.
*Done when:* one template has 10+ clones scheduled.

**Phase 4 — Repurposing (only for proven winners, ~1 hr/winner):** P4 → 1 carousel (Canva free) → IG; 1 faceless video (CapCut, text-overlay, no voice) → TikTok+Reels; bio points to Beacons (single-product-per-post beats bio-choice-paradox per playbook). Log as `car`/`vid` rows with same serial root.
*Done when:* 2–3 winners repurposed and logged.

**Phase 5 — Cadence (ongoing):** weekly batch + 2 check-ins + monthly P5 review. Upgrade triggers ONLY: scheduler paid if free queue overflows 2+ months AND EPC-positive; custom Postgres only on §5 trigger. Otherwise hold the line — low friction is the strategy.

---

## 9. Pitfalls (from playbook + beginner failure modes)

1. Links in post body → reach dies. Comments only.
2. Day-one link spam on fresh accounts → throttle/flag. Warm up 7 days link-free.
3. Reusing tags across posts → attribution garbage. One post, one tag.
4. Hand-typing tags into Sheets → join breakage. Copy-paste only.
5. Claiming you tested products you did not → trust + policy risk. Use rating/comment-anchored language.
6. Reading GMV as your money → it is not. Commission (approved) is your money; pending is not yet yours.
7. Two niches at once / daily format-hopping at 3–5 hrs/week → no signal. One niche, one template until 30 days of data.
8. Building a tracker app before 150 posts → the classic side-project killer. Sheet first, always.

---

## 10. Start-today action list (next 60 minutes)

1. Register Shopee Affiliate + open link-builder + reports screens (20 min).
2. Write down your tag convention `th_a1_t001_txt` on paper/Sheet (2 min).
3. Create Threads + X accounts, post 1 link-free value post each (20 min).
4. Create the Google Sheet with the 3 tabs + columns in §5 (10 min).
5. Run P1 in Claude, save the idea bank to the Sheet (8 min).

Provenance: built from an organic-growth playbook for Shopee Affiliate (X thread, background reference only), specified for a from-zero, ~3–5 hrs/week, faceless operator, then hardened against `research/shopee-affiliate-workflow-research.md` (69 primary-source citations, compiled 2026-09-13). Defaults (niche, tracker, LLM) are marked wherever they appear — swap them for yours.

## Addendum A — Primary-source corrections applied (2026-09-13)
1. Payout is WEEKLY (not monthly): <Rp500.000 via ShopeePay, ≥Rp500.000 via bank transfer, PPh 21/26 withheld, KTP/NPWP required before payout. Sources: Terms §§5.1–5.4.
2. Indirect orders pay HALF the set rate (direct = full rate). 7-day click→order window confirmed. Do not model every order at full rate. Sources: seller-edu 11239 + 11241 FAQ.
3. No official CSV export on the individual affiliate Performance Report — monthly review = manual copy/screenshot of Klik/Pesanan/Produk Terjual/Pesanan(Rp)/Komisi Kotor(Rp) into Sheets. Do not plan a CSV pipeline.
4. "≥3 tags" is convention, not rule — tags exist as free-form tracking parameters with per-tag click reports, no official count/length limit documented; custom-link manipulation (masking/mass-blast) voids commission. One post = one tag still holds as hygiene.
5. Paid ads are not blanket-banned but require prior Shopee approval; clickbait paid ads, self-purchase via own link, multi-accounting, and fake-promotion/clickbait are explicit violations with non-payment/freeze penalties.
6. Scheduler verdict hardened: Buffer Free (3 channels, 10 queued/channel, Threads+X supported, Start Page link-in-bio included, first-comment scheduling NOT on free) is primary; Publer Free runner-up; Later and Hootsuite have NO free plan; Metricool Free caps at 20 posts/mo. Link-in-comment stays a 30-sec manual phone step on any free tier.
7. Platform ceilings (first-party): Threads 500 chars / 250 posts + 1,000 replies per 24h / max 5 links per post; X free accounts 50 posts + 200 replies/day. No official Meta/X doc confirms in-feed link suppression — treat as unverified community lore; comments-only placement stands as risk hedge, not documented rule.
8. Dashboard refreshes daily at 16:30 WIB, 1-year lookback, product ranking to 1,000 products, commission split (Xtra/Seller/MCN/Shopee). Category rate tables in blogs are unverified — only "up to 10% + unlimited XTRA" is official; read per-product rates in your own portal.

## Appendix B — Check-in checklist (25 min, 2x/week) + warm-up starters

Run this verbatim each check-in. No improvisation needed.

- [ ] **5 min — queue health:** Buffer queue still ≥2 days deep? If not, generate the gap posts with P2 now.
- [ ] **10 min — first-comment links:** every post published since last check-in gets its ONE tagged link as your own first comment/reply within the window. Copy the link from the Sheet (never retype the tag).
- [ ] **5 min — replies:** answer every comment on your posts; drop 5–10 replies on in-niche accounts. No links in any reply except your own first comments.
- [ ] **5 min — numbers:** record views/likes/replies per post in the Sheet. Any post >3x your median views → flag as winner candidate, feed to P3 immediately (do not wait for month-end).

**Warm-up starters (days 1–7, link-free — copy, adapt, post; more in `../docs/content-examples.md`):**

1. Story/relatable: "Kamar kos 3x3 aku dulu gudang + kamar + dapur jadi satu. Yang pertama aku beresin bukan decluttering, tapi zonasi: tidur, masak, kerja. Besok aku spill urutannya."
2. Practical list: "3 barang under 50rb yang paling sering direkomendasikan penghuni kos di kolom komentar: 1) gantungan tempel tanpa paku, 2) kotak transparan kecil, 3) lap microfiber 5-pack. Kalian nambahin apa?"
3. Mistake post: "Kesalahan paling umum nata dapur sempit: beli storage dulu sebelum ngukur. Ukur lebar rak + tinggi kolong dulu, baru pilih wadahnya. Aku pernah salah beli 2x."

## Appendix C — Troubleshooting (symptom → cause → fix)

1. **0 clicks after 2 weeks of linked posts** → cause: links never seen (reach problem, not product problem). Fix: check views first — if views ~0, it's account/reach (warm-up skipped? links in post body? posting >3/day on a new account?). If views exist but clicks ~0, the comment link is missing/late or the post topic has no buying intent — move the comment inside 15 min and tighten topic-to-product match.
2. **Views suddenly collapse** → cause: velocity or spam flag. Fix: drop to 1/day for a week, zero links for 3 days, only replies + value posts. Never mass-delete posts (looks worse).
3. **Clicks exist, commission 0** → normal early on: commission counts only completed + validated orders; dashboard shows gross estimates first. Wait one full weekly payout cycle before judging. If persists 30 days with clicks, the traffic has no buying intent — change product category, keep the format.
4. **Tag missing in Click Report** → cause: link generated with "Pakai Tag: Tidak", or tag retyped with a typo. Fix: regenerate with Ya + copy-paste; correct the Sheet row. Never reuse that broken tag.
5. **Payout stuck / "Tertunda" / "Perlu Lengkapi"** → cause: almost always identity/bank docs (KTP/NPWP mismatch, account-name mismatch). Fix: re-check name match + doc status in dashboard, watch email. Money under Rp500rb goes to ShopeePay — verify ShopeePay KYC too.
6. **Account warning / link removed** → cause: spam pattern (link in post body, DM blasting, mass-blast custom links) or prohibited product. Fix: stop all links 7 days, delete only the flagged post, re-read Terms §§5.2/6.3, resume at half velocity.
