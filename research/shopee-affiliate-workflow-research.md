# Shopee Affiliate Indonesia — End-to-End Workflow Research (Primary Sources)

**Date compiled:** 13 September 2026
**Scope:** Primary-source grounding (official help centers, terms, pricing pages) for: Shopee Affiliate Indonesia program mechanics; free-tier scheduling tools; free-tier tracking tools; supporting creative/link tools; Threads/X first-party platform rules; conditional Postgres fallback.
**Method note:** All factual claims carry an inline citation to the page they were read from. Where an official source could not be reached or does not exist, that is flagged explicitly as **UNVERIFIED** rather than filled with blog numbers. `affiliate.shopee.co.id` is a JavaScript app that cannot be fetched by a text client — its UI details are flagged where relevant.

---

## TL;DR Verdicts

| # | Question | Verdict |
|---|----------|---------|
| 1 | Shopee Affiliate ID: how do registration / payout / commission actually work? | Confirmed from official terms: register via app "Saya" tab or affiliate.shopee.co.id, ~1 working-day review, no minimum followers. **Payouts are WEEKLY**, not monthly — below Rp500,000 goes to ShopeePay, at/above goes to bank transfer, and **PPh income tax is withheld** (KTP/NPWP required). 7-day click→order window confirmed; indirect orders earn **half** the commission rate. |
| 2 | Does the official program contradict the playbook? | Partly. The 7-day cookie, link-tool usage, and organic-first approach all check out. Contradictions: (a) payout cadence is weekly not monthly; (b) the "≥3 tags" link convention has **no official documentation** (tags exist but limits are undocumented); (c) paid ads are not blanket-banned but **require prior Shopee approval**, and clickbait paid ads are banned; (d) self-purchase via your own link is banned. |
| 3 | Best free scheduler for 1-person Threads batch posting? | **Buffer Free** (3 channels, 10 queued posts/channel, Threads + X + IG + FB support, free Start Page link-in-bio). Runner-up **Publer Free** (3 accounts, 10 pending/account). **Later and Hootsuite have NO free plan** (trial only). Metricool Free caps at 20 posts/month total. |
| 4 | Tracking stack? | **Google Sheets** (free, 10M cells, 15 GB Drive) is sufficient and is the recommendation. A custom Postgres tool is **NOT justified** at current scale; revisit only if triggers in §3.4 fire. |
| 5 | Threads/X platform constraints (first-party)? | Threads: 500 chars, max 250 posts + 1,000 replies per 24h, **max 5 links per post** (from 22 Dec 2025). X free accounts: **50 original posts + 200 replies per day** (semi-hourly sub-limits). No official Meta/X doc confirms "links are suppressed in-feed" — that belief is community-reported, not documented. |
| 6 | Link-in-bio / carousel / video tools free tier? | Linktree Free (unlimited links, basic analytics) or **Buffer Start Page (free, already included)**; Canva Free (5 GB, 1.6M+ templates, Brand Kit 3 colors only); CapCut free tier works for basic short-video editing but **free cloud sync was discontinued Aug 2024** and premium assets are Pro-gated. |

---

## 1. Shopee Affiliate Indonesia (Program Mechanics)

### 1.1 Registration & eligibility
- Three official registration channels: (1) search "Shopee Affiliate Program" in the Shopee app, (2) the **"Saya" (Me) tab** in the Shopee app, (3) the website at affiliate.shopee.co.id; approval is confirmed by notification + email. — [Help: How to register](https://help.shopee.co.id/portal/4/article/72050-%5BShopee-Affiliates-Program%5D-Bagaimana-cara-mendaftar-Shopee-Affiliates-Program%3F)
- Fill the form at affiliate.shopee.co.id with your Shopee account; account review takes **up to 1 working day**; **no minimum followers/subscribers requirement**. Recommended products: stores with Mall, Shopee Supermarket, Star+, Star Seller badges. Prohibited products include tobacco/vape, drugs, adult/pornographic and counterfeit goods. — [Official landing: Cara Daftar Shopee Affiliate](https://shopee.co.id/m/daftar-affiliate)
- Legal basis: any individual may apply; Shopee can accept or reject applications at its discretion after verifying the participation form. — [Terms for Individuals §2.1](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)

### 1.2 Payout (threshold, method, tax)
- **Weekly payment cadence:** "Biaya Jasa … akan dibayarkan oleh Shopee kepada Partisipan **setiap minggu** dan melalui transfer bank ke rekening bank terdaftar milik Partisipan. … untuk pembayaran di bawah **Rp500.000**, pembayaran akan dilakukan melalui akun **ShopeePay**." — [Terms for Individuals §5.1](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- **Tax withholding:** commission is paid gross of PPh; Shopee **withholds PPh Pasal 21/26**; the affiliate must submit **KTP and/or NPWP** copies — without them, payout cannot be processed. — [Terms for Individuals §5.2–5.4](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- ⚠️ **Playbook correction:** the playbook assumed monthly review → that is fine for *analysis*, but money moves **weekly**, and the "threshold" is really a method switch (ShopeePay vs bank), not a monthly minimum. Many third-party blogs claim "monthly payout, Rp100k minimum" — that matches a different aggregator (e.g., Accesstrade) and **not** Shopee's own first-party program terms.

### 1.3 Commission model
- Commission = **commission rate × Net Completed Purchase Value** (order value minus discounts, shipping, vouchers, Shopee Coins, etc.). Rates are set per-product by sellers (Pay-Per-Sale). — [Terms for Individuals §3.4](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu) and [Seller AMS Terms §4.1](https://help.shopee.co.id/portal/4/article/73983)
- **Two rate families exist** (set by sellers): *KomisiXTRA Produk* (open to all affiliates) and *KomisiXTRA Khusus* (targeted at specific affiliates; must be higher than the product commission). — [Seller education: AMS commissions](https://seller.shopee.co.id/edu/article/11241)
- **Direct vs indirect orders:** official seller-side mechanism table — *Pesanan Langsung* (buyer checks out the promoted product straight from the affiliate link) pays the full set rate; *Pesanan Tidak Langsung* (buyer clicks your link, then checks out a different product via Shopee's recommendation) pays **half** of the set rate. — [Seller education: Mekanisme Perhitungan Komisi AMS](https://seller.shopee.co.id/edu/article/11239)
- **7-day window confirmed:** "Jika Pembeli klik link Affiliate dan melakukan pesanan dalam 7 hari, pesanan tersebut akan dianggap sebagai transaksi Affiliate." — [Seller education: AMS FAQ](https://seller.shopee.co.id/edu/article/11241). Corroborated for the seller-affiliate variant: commission for checkouts within **7 calendar days** of link click. — [Seller education: Program Afiliasi Penjual](https://seller.shopee.co.id/edu/article/8174/afiliasi-penjual-shopee)
- Headline rates (official marketing copy): "komisi hingga **10%** dan komisi XTRA dari brand tanpa batas" (up to 10% + unlimited brand XTRA commissions). An older official Shopee blog (2022) cited "Komisi Shopee hingga 4% for all orders" — treat that as outdated; use the current landing figure. — [Inspirasi Shopee blog, 2022](https://shopee.co.id/inspirasi-shopee/shopee-affiliates-program/) — [Cara Daftar Shopee Affiliate](https://shopee.co.id/m/daftar-affiliate)
- **No commission** for: cancelled/incomplete/returned/refunded orders; self-purchase via your own link; fraud-detected transactions; reselling schemes; transactions from untraceable sources (ad networks, x-rated/porn sites); **digital products**; repeated violations. — [Terms for Individuals §3.4, §5.2](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- **Komisi XTRA rate protection:** if a seller *lowers* a rate, an affiliate meeting protection criteria keeps the original rate for **7 calendar days**. — [Seller education: AMS mechanism](https://seller.shopee.co.id/edu/article/11239)
- ⚠️ **UNVERIFIED:** a category-by-category commission-rate table (e.g., "fashion 7–10%") circulates in blogs but I found **no first-party category table**. Rates are visible per product in the affiliate app/portal. Do not build the plan on blog rate tables.

### 1.4 Dashboard: what columns actually exist
Official help article for the **affiliate** Performance Report ("Laporan Performa"):
- **Klik** (total clicks from affiliate links + products pinned in Live/Video), **Pesanan** (orders incl. not-yet-completed/unvalidated), **Produk Terjual** (commissioned products sold), **Pesanan (Rp)** (total order value), **Komisi Kotor (Rp)** (gross estimated commission before validation).
- Data refreshes **daily at 16:30 WIB**; selectable period up to **1 year**; four report views (All / Live / Video / plus content view); *Performa Produk* ranks up to **1,000 products** by orders/sales/commission; *Rincian Komisi* breaks down Komisi Xtra, Komisi Penjual, Promo MCN, Komisi Shopee. Gross estimates differ from the final *Laporan Komisi* because **commission only materializes for completed, validated orders**. — [Help: Laporan Performa Shopee Affiliate](https://help.shopee.co.id/4/article/123077-%5BShopee-Affiliate-Program%5D-Apa-itu-Laporan-Performa-Shopee-Affiliate-dan-bagaimana-cara-membaca-Laporan-Performa)
- **Payment statuses** are enumerated in the seller-side affiliate docs: *Perlu Lengkapi (payment data incomplete) / Divalidasi / Menunggu Dibayar / Tertunda / Ditolak* — a reasonable template for what the affiliate app shows (app shows tabs: Semua, Sedang Divalidasi, Menunggu Dibayar, Dibayarkan, Tertunda, Ditolak per the same article's app section). — [Seller education: Program Afiliasi Penjual — Laporan Komisi](https://seller.shopee.co.id/edu/article/8174/afiliasi-penjual-shopee)
- ⚠️ **UNVERIFIED:** exact payment-status tab names inside the *individual* affiliate app — the official article enumerates statuses for the seller-affiliate program; the individual-app tab list is not documented in the help-center article I could reach.
- ⚠️ **CSV/Export UNVERIFIED:** no official help article documents a **CSV export button** on the individual affiliate Performance Report. Seller-side reports have downloadable invoices/tax documents ([AMS FAQ reports table](https://seller.shopee.co.id/edu/article/11241)). **Plan implication:** design the monthly raw-report review around manual copy of the dashboard's numbers (or app screenshots) into Sheets, not around a CSV pipeline.

### 1.5 Link creation flow & tagging
- Official flow (affiliate side): pick a product → generate the affiliate link → share; the landing page explicitly lists placing links in TikTok bio/caption, Instagram swipe-up, YouTube description, **link inside a Twitter/X thread**, Facebook posts. — [Cara Daftar Shopee Affiliate](https://shopee.co.id/m/daftar-affiliate)
- **Tags are real and official:** for the affiliate link tool, "Tag link: Kode tambahan sebagai parameter pelacakan link afiliasi" (an extra tracking parameter); you can convert up to **5 Shopee links per batch**; the Click Report exposes per-custom-link performance via a "Pakai Tag" field. — [Seller education: sharing links](https://seller.shopee.co.id/edu/article/8173) and [Program Afiliasi Penjual — Laporan Klik](https://seller.shopee.co.id/edu/article/8174/afiliasi-penjual-shopee)
- ⚠️ **UNVERIFIED for the individual program:** the individual-affiliate portal's custom-link ("Link Khusus") flow — including whether there's a "Pakai Tag: Ya/Tidak" toggle and any tag count/length limits — is **not documented** in the help center pages I could reach. Third-party walkthroughs describe a tag toggle and an optional free-form tag name, which matches the terms' definition of tracking-parameter tags, but **no official limit exists**. Practical guidance: use short lowercase tags (platform/account/content type) and verify the toggle inside the portal on day one. **Do not adopt the playbook's "≥3 tags" as an official requirement — it is a convention, not a rule.**
- **Custom-link misuse is a violation:** promoting via masking, mass-blasting, or using the custom-link feature "in ways not per Shopee's stipulations … to manipulate users or to obtain maximum reach with nonspecific/irrelevant targeting" voids commission and can end participation. — [Terms for Individuals §6.3(o)](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)

### 1.6 Policy pitfalls (spam, claims, paid ads)
From the individual terms and the violations article:
- **Non-commissionable transactions include** spamming links to irrelevant recipients, "ads without prior Shopee approval," and irrelevant/clickbait placements. — [§5.2(f)](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- **Prohibited behaviors** include: email ads without written approval; multiple accounts; bots/automated queries; fraudulent SEO; clickbait spam ("promosi palsu … ulasan produk yang bersifat clickbait"); sharing links without content or repeating identical content to the same audience; **keyword ads using the "Shopee" brand** without written approval (Shopee must be an excluded/negative keyword); scraping Shopee IP/assets; links on torrent/streaming sites; **paid ads used in clickbait fashion to farm clicks**; stealing other affiliates' content; ads imitating Shopee identity. — [§6.3](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- **Penalties:** Shopee may warn, block, refuse to pay, claw back paid commission, freeze/suspend, or terminate accounts; the dedicated violations article (penalty matrix is in images) confirms penalties per violation type. — [§6.5](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu) + [Help: Jenis pelanggaran dan penalti](https://help.shopee.co.id/portal/10/article/123212)
- ⚠️ **"Fake testimonial" as a named rule:** the individual terms do **not** contain a clause literally titled "fake testimonials." The closest official language bans *promosi palsu* (fake promotion) and clickbait product reviews, plus the general anti-manipulation clause (§5.2(l), §6.3(r)). Under the general Shopee Service Terms (incorporated by reference) misleading content would also violate platform policy. **Playbook rule "no fake testimonials" is sound but should be mapped to the anti-fake-promotion/anti-clickbait clauses, not quoted as a distinct named rule.**
- **Paid ads ≠ total ban, but effectively out of scope for this project:** ads require **prior Shopee approval** (§5.2(f)); clickbait paid ads are banned outright (§6.3(n)); brand-keyword ads banned (§6.3(h)). Organic-only, as the playbook assumes, is compliant by default. — [Terms for Individuals](https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu)
- ⚠️ **Playbook "0.5% click→order hit rate"**: **no official source**; it is a practitioner heuristic. Treat as an assumption to be replaced by your own measured numbers within ~2 months of data.

---

## 2. Scheduling Tools (official pricing/docs, checked 13 Sep 2026)

### 2.1 Buffer — **RECOMMENDED (free tier fits the job)**
Source: [buffer.com/pricing](https://buffer.com/pricing) (live page, features table):
- Free plan: **3 channels**, **10 scheduled posts per channel** (queue slot refills as posts publish — "refill anytime"), **100 ideas**, 1 user, **AI Assistant included**, Insights with 30-day history, **Start Page included** (link-in-bio page that counts as a channel), API access (1 key, 3,000 req/mo), threaded posts limited to 1.
- **First comment scheduling is NOT on Free** (Essentials+, and per the feature description only for Instagram, Facebook, LinkedIn).
- **Threads profiles: Automatic Publishing Included**, basic analytics included, community engagement (reply to comments) included. X/Twitter free profiles: automatic publishing included. TikTok/IG/FB/YouTube/Bluesky/Pinterest/LinkedIn/Mastodon/GBP all supported on Free.
- Paid starts at $5/month per channel (Essentials, billed yearly) if you later want unlimited queue + first comments.
- Verdict: for **1 person, text-first Threads posts (~20–40/month)**, 10 queue slots per channel is sufficient with a weekly top-up; Threads auto-publishes from the queue. The **link-in-comment step is manual** on Free (no first-comment scheduling) — post the Shopee link as your own first comment right after publishing (phone notification workflow). Bonus: Start Page doubles as the free link-in-bio.

### 2.2 Metricool
Source: [metricool.com/pricing/](https://metricool.com/pricing/) (live page):
- Free: **1 brand**, all networks **except LinkedIn and Twitter/X**, **20 scheduled posts per month** (total), 5 competitor profiles, 30-day analytics, AI assistant.
- Verdict: 20 posts/month total is too tight for a volume game (7-day cookie ⇒ want daily posting). Threads IS supported on Free; X is not.

### 2.3 Later — **NO free plan**
Source: [later.com/pricing/](https://later.com/pricing/) (live page): plans are Starter ($18.75/mo billed yearly), Growth, Scale — all behind a **14-day free trial**; no free tier listed. Starter = 1 social set (8 profiles incl. Threads), 30 posts per profile/month. Threads auto-publish supported on all plans.
- Verdict: excluded on the "usable free tier" constraint.

### 2.4 Hootsuite — **NO free plan**
Sources: [hootsuite.com/pricing](https://www.hootsuite.com/pricing) and [hootsuite.com/plans](https://www.hootsuite.com/plans) — Standard $99 / Professional $199 / Advanced $399 per user/month (annual billing), all behind a 14-day trial ("No credit card required" for trial; trial accounts have 10–20 posts/day limits). The company help center's plan-management article (updated March 2026) confirms current plan structure. — [help.hootsuite.com: plan & account](https://help.hootsuite.com/s/article/plan-account)
- Verdict: free plan was dropped in 2023 and has not returned; excluded.

### 2.5 Publer — **runner-up**
Sources: [publer.com/plans](https://publer.com/plans), [Publer help: What is included in Publer Free](https://publer.com/help/en/article/what-is-included-in-publer-free-dliovh/), [Publer help: plans & pricing](https://publer.com/help/en/article/what-are-publers-plans-and-pricing-15h4yqh/), [rate limits doc](https://publer.com/docs/getting-started/rate-limits):
- Free: **3 social accounts, excluding Twitter/X** (X requires a paid tier due to API cost), **10 pending scheduled posts per account (30 total)** — a slot frees when a post publishes or is deleted, 25 drafts, **24-hour posts history** (older published posts are not stored server-side), Instagram link-in-bio.
- **Threads is supported on Free** — the rate-limit table allows **150 Threads posts/day/profile on Free** (vs 250 API ceiling; platform compliance).
- The plans page lists "Schedule 1st comments & threads" among features, but the page text does not unambiguously bind that feature to the Free tier (an adjacent note excludes "automation policies … while on a free plan"). ⚠️ **Verify in-app whether first-comment scheduling works on Free before relying on it.**
- Paid starts at $5/mo (Professional, 1 account).

### 2.6 "Anyone who dropped Threads free support?"
- **Later and Hootsuite dropped/never restored free plans entirely** (see above) — so they don't even have a free tier in which Threads support could matter. No evidence found (and none needed) of a tool keeping a free plan while removing Threads specifically: **Buffer Free, Metricool Free, and Publer Free all still support Threads** as of the September 2026 pricing pages cited above.

### 2.7 Recommendation
**Buffer Free** is the primary: it uniquely combines (a) Threads auto-publish, (b) X support (nice if you later mirror to X within the 50-posts/day free cap), (c) a free Start Page link-in-bio, (d) an AI assistant on Free, and (e) queue semantics (10/channel) that match a "batch every 3–4 days" cadence. **Publer Free** is the fallback if you need first-comment scheduling and can confirm it works on Free. Manual link-in-comment remains a 30-second phone action either way.

---

## 3. Tracking / No-Code Tools

### 3.1 Google Sheets — **RECOMMENDED**
- Free with a Google account; storage is the binding constraint: **15 GB shared across Gmail/Drive/Photos**. — [Google storage works](https://support.google.com/drive/answer/9312312)
- Capacity: **up to 10 million cells or 18,278 columns** per spreadsheet (same for imported CSV/Excel). — [Files you can store in Google Drive](https://support.google.com/drive/answer/37603)
- Scale check: 30 posts/month × 12 months × ~10 columns ≈ 3,600 cells/year — four orders of magnitude below limits. CSV pastes from dashboard copies are trivially ingested (import limits identical per the same doc).

### 3.2 Notion — usable, not ideal for joins
Source: [notion.com/pricing](https://www.notion.com/pricing) (live page):
- Free: **unlimited pages & blocks for individual** workspaces (block-limited only for 2+ members), file uploads **capped at 5 MB per file**, page history **7 days**, 10 guests, **1 chart**, basic forms, basic automations (buttons only).
- Verdict: fine as a content-idea/creative library, but relational rollups across a posts table + a performance-import table are weaker than Sheets formulas (XLOOKUP/QUERY) for the "join Shopee numbers to posts" job.

### 3.3 Airtable — free tier exists; numbers not on the pricing page
Source: [airtable.com/pricing](https://airtable.com/pricing) (live page): Free plan exists ("formulated for individual users, very small teams, or those with lightweight needs"), per-seat billing above it (Team $20/user/mo annual); FAQ confirms overage behavior (can't add records past limit; data never deleted).
- ⚠️ **UNVERIFIED:** Airtable's pricing page does **not state** its free record/attachment caps (historically 1,000 records/base, but not printed on the page I fetched — do not rely without checking [support.airtable.com billing overview](https://support.airtable.com/docs/airtable-billing-overview)). For a monthly-updated log this is unlikely to bite within year one, but it's an avoidable risk.

### 3.4 Minimal data model (sized to need) — canonical definition lives in plan §5; import-ready templates in `tracking/`
Three tabs, all in one spreadsheet, mirroring exactly the dashboard columns the official report exposes (§1.4):
1. **posts** — `post_id (PK)`, `date_posted`, `platform` (th/x/ig/tt), `account`, `format` (txt/car/vid), `post_url`, `hook_first15words`, `template`, `topic`, `shopee_tag (UK, exact string)`, `shopee_product_url`, `views`, `likes`, `replies`, `notes`.
2. **links** — `shopee_tag (PK)`, `product_name`, `product_url`, `price_band`, `category`. (Your own bookkeeping mirror of the Shopee tag parameter — see §1.5 caveat that Shopee doesn't document tag limits.)
3. **performance_import** — `month`, `shopee_tag (FK)`, `klik`, `pesanan`, `produk_terjual`, `pesanan_rp`, `komisi_kotor_rp`, `post_id` (VLOOKUP from tag), `notes`, plus the copy date/time (dashboard refreshes 16:30 WIB).
Join: monthly `performance_import` → `posts` via `shopee_tag`; pivot by platform × format × template → clicks, orders, commission, EPC. Nothing more is needed.

### 3.5 Is a custom Postgres tool justified? **NO (for now).**
Arguments against building now: (a) data volume is ~10³ rows/year vs Sheets' 10⁷-cell capacity ([Google limits](https://support.google.com/drive/answer/37603)); (b) the only ingest path is **manual** (no official Shopee CSV/API for individual affiliates — §1.4 caveat), so software adds zero automation; (c) maintenance burden (auth, hosting, backups) is pure drag on a side project; (d) AI analysis of a monthly raw report works on pasted text regardless of storage.
**Revisit triggers** (any one): >5,000 perf rows or >1 import source; need for multi-year cohort queries Sheets can't express; more than one person joining data; Shopee ever exposes a real export/API for individuals.

---

## 4. Supporting Free-Tier Tools

### 4.1 Link-in-bio
- **Buffer Start Page — included free** on the Free plan (counts as one of your 3 channels). — [buffer.com/pricing](https://buffer.com/pricing)
- **Linktree Free:** unlimited links, core appearance options, basic analytics; paid tiers add scheduling/analytics/branding removal. — [linktr.ee/pricing](https://linktr.ee/pricing)
- Verdict: since you're adopting Buffer anyway, **Start Page costs zero extra channels-of-attention**; Linktree is the standalone fallback. (Beacons.ai: not verified — skipped rather than quote unverified numbers.)

### 4.2 Carousel design — Canva Free
Sources: [canva.com/en_us/pricing/](https://www.canva.com/en_us/pricing/) and [Canva Help: manage uploads](https://www.canva.com/help/manage-uploads/):
- Free includes: drag-and-drop editor, 1,000+ design types, **1.6M+ free templates**, 4.7M+ free photos/videos/graphics/audio, **1 Brand Kit limited to 3 colors**, **5 GB cloud storage**, up to **200 Standard / 20 Premium AI uses**.
- Free folders hold up to **200 items**; storage-full notification at 80%. — [Canva Help: uploads](https://www.canva.com/help/manage-uploads/)
- Gotcha: **premium templates/elements are Pro-gated** — a design using them won't export cleanly on Free. Official pages don't document an export *watermark* for free-tier content; the practical failure mode is the Pro upsell on premium assets, not a stamp. (UNVERIFIED beyond that: any hard watermark policy claim.)

### 4.3 Short-video editing — CapCut (free/Standard tier)
Sources: [CapCut help: Standard vs Pro](https://www.capcut.com/help/capcut-standard-vs-pro), [CapCut resource: Standard vs Pro](https://www.capcut.com/resource/capcut-standard-vs-pro), [pricing change notice](https://www.capcut.com/help/pricing-change), [Pro cost FAQ](https://www.capcut.com/help/how-much-does-capcut-pro-cost):
- Free/Standard: basic editing (cut/trim/merge/split), free filters/transitions/effects, text & stickers, basic audio; "Standard" is positioned for casual social-media creators.
- Gotchas: **free cloud storage for projects was discontinued (Aug 2024)** — projects live on-device; premium templates/effects/fonts/music and advanced AI (auto-captions, background removal, motion tracking) are **Pro-only**; Pro price **varies by region/device** (no fixed global price published).
- No official free export-count or resolution cap is documented on the pages fetched (UNVERIFIED whether regional builds differ).

---

## 5. Threads & X Organic Best Practice — First-Party Sources Only

### 5.1 Threads (Meta first-party)
- **Character limit: 500** per post (uniform for posts/replies/quotes). — [Threads API docs: posts](https://developers.facebook.com/docs/threads/posts/) (also [overview](https://developers.facebook.com/docs/threads/overview/))
- **Publishing ceilings:** **250 published posts / 24h** and **1,000 replies / 24h** per profile (API-enforced; carousels count as one post). — [Threads API overview](https://developers.facebook.com/docs/threads/overview/)
- **Links:** posts **may include links** (Meta's own announcement) — [about.fb.com, Jul 2023](https://about.fb.com/news/2023/07/introducing-threads-new-app-text-sharing/); API doc: **max 5 links per post** from **22 Dec 2025** (posts with >5 unique links fail), link-attachment preview available for text-only posts. — [Threads API docs: posts](https://developers.facebook.com/docs/threads/posts/)
- ⚠️ **Link suppression is NOT officially documented.** No Meta help/dev page states that link-containing posts are down-ranked in feed. The widespread belief that links reduce reach is community-reported. What *is* first-party: links are allowed, render previews, ≤5 per post. **Playbook's "link only in comments" remains a sensible hedge, but should be framed as an unproven best practice, not a platform rule.** Re-run an A/B (link-in-post vs link-in-comment) after ~60 posts.
- ⚠️ **New-account flagging:** Meta does not publish restriction thresholds for new Threads accounts. Third-party reports describe 24–72h automated restrictions tied to rapid following/posting and young/low-trust Instagram accounts (e.g., [WiseChecker analysis, May 2026](https://wisechecker.com/threads-account-restricted-new-signup/)) — **treat as anecdote**; the first-party takeaway is simply: warm up gradually, don't mass-follow/burst-post on a fresh account.
- Practical ceiling for this project: even 10 posts/day is 4% of the 250/day cap — the platform limit will never bind; content quality and consistency are the real constraints. **No official posting-frequency *recommendation* exists from Meta.**

### 5.2 X (first-party help page, fetched 13 Sep 2026)
Source: [Understanding X limits — help.x.com](https://help.x.com/en/rules-and-policies/x-limits):
- **Unverified (free) accounts: 50 original posts + 200 replies per day**, with additional **semi-hourly sub-limits**; limits apply across all devices and third-party apps.
- Also: 500 DMs/day; 400 follows/day; follow attempts restricted past 5,000 following (ratio-based); email changes 4/hour. Limits may tighten further during heavy load; hitting a limit surfaces an explicit error message.
- For the playbook: mirroring Threads winners to X is feasible (10–20 posts/day ≪ 50), but X organics on a free account are rate-capped by design; treat X strictly as a repurposing channel.
- ⚠️ Legacy behavior note: X historically re-writes all URLs through t.co; the current limits page no longer discusses link handling, so **no first-party statement about link ranking on X** could be cited. Same posture as Threads: link-in-comment as hedge, measure your own numbers.

---

## 6. Conditional Fallback: Postgres Stack (ONLY if §3.5 triggers fire)

If a custom tracker ever becomes justified, the boring-and-debuggable choice:
- **Next.js 15 (App Router, TypeScript) + Drizzle ORM + PostgreSQL + Tailwind + shadcn/ui**, deployed on Vercel with a managed Postgres free tier (Neon or Supabase — verify current free-tier terms before committing; not quoted here as prices move).
- Justification: one language end-to-end (TS) → one debugging mental model; Drizzle gives typed, inspectable SQL (easy to debug vs magic-heavy ORMs) while remaining a mainstream, hugely-documented choice; Prisma is the equally mainstream alternative if you prefer richer tooling (`prisma studio`) over raw-SQL ergonomics; shadcn/ui ships copy-paste components so the UI is never a black box; Next.js is the single most-documented React meta-framework, maximizing AI-assisted and human debugging quality. All of these are free/open-source; the only paid component ever needed is managed Postgres if free tiers are outgrown.
- Effort guardrail: this is a **2–4 weekend** build — do not start it before the Sheets tracker has 3 months of real data.

---

## Open Questions & Uncertainties (explicit flags)

1. **Individual-affiliate custom-link flow & tag limits** — tags are officially real (tracking parameters, per-custom-link click reporting) but the individual portal's tag UI/limits are undocumented in reachable help-center pages. Verify the "Pakai Tag" toggle and custom-link menu inside affiliate.shopee.co.id on day one. No official "≥3 tags" rule exists.
2. **CSV/export on the individual affiliate dashboard** — unconfirmed. Plan for manual monthly transcription of raw numbers into Sheets.
3. **Affiliate-app payment-status names** — seller-side statuses are documented; individual-app tab names are not (adopt seller-side as the working vocabulary).
4. **Category commission-rate tables** — no first-party table; only "up to 10% + KomisiXTRA" is official. Read per-product rates in the app.
5. **Threads link down-ranking & new-account thresholds** — community-reported, not Meta-documented; treat as hypotheses to A/B, not rules.
6. **X link handling (t.co, link ranking)** — no current first-party statement found on the limits page.
7. **Publer Free first-comment scheduling** — plans-page attribution ambiguous; confirm in-app before switching from Buffer.
8. **Airtable Free numeric record cap** — not stated on the pricing page; check support docs before adopting Airtable.
9. **Playbook heuristics with no official source:** 0.5% click→order hit rate; "≥3 tags"; monthly payout assumption (actually weekly). Replace with measured data within ~60 days.
10. **affiliate.shopee.co.id UI details** — the portal is a JS app; in-app screens (dashboard tabs, link builder) could not be verified from outside. Everything program-legal above comes from help.shopee.co.id / shopee.co.id text pages.

---

## Source List (primary sources; all accessed 13 Sep 2026)

**Shopee (first-party):**
- Terms for Individuals (Syarat dan Ketentuan Program Afiliasi Shopee untuk Individu): https://help.shopee.co.id/4/article/71217-Syarat-dan-Ketentuan-Program-Afiliasi-Shopee-untuk-Individu
- Violations & penalties: https://help.shopee.co.id/portal/10/article/123212
- How to register: https://help.shopee.co.id/portal/4/article/72050-%5BShopee-Affiliates-Program%5D-Bagaimana-cara-mendaftar-Shopee-Affiliates-Program%3F
- Affiliate Performance Report columns: https://help.shopee.co.id/4/article/123077-%5BShopee-Affiliate-Program%5D-Apa-itu-Laporan-Performa-Shopee-Affiliate-dan-bagaimana-cara-membaca-Laporan-Performa
- Official registration landing: https://shopee.co.id/m/daftar-affiliate
- Seller-side AMS terms: https://help.shopee.co.id/portal/4/article/73983
- AMS commission mechanism (direct vs indirect): https://seller.shopee.co.id/edu/article/11239
- AMS overview & commissions (XTRA types, 7-day window FAQ, reports): https://seller.shopee.co.id/edu/article/11241
- Seller-Affiliate link sharing & tag parameter: https://seller.shopee.co.id/edu/article/8173
- Seller-Affiliate program & reports (statuses, click report per tag): https://seller.shopee.co.id/edu/article/8174/afiliasi-penjual-shopee

**Scheduling tools (official pricing/docs):**
- Buffer: https://buffer.com/pricing
- Metricool: https://metricool.com/pricing/
- Later: https://later.com/pricing/
- Hootsuite: https://www.hootsuite.com/pricing ; https://www.hootsuite.com/plans ; https://help.hootsuite.com/s/article/plan-account
- Publer: https://publer.com/plans ; https://publer.com/help/en/article/what-is-included-in-publer-free-dliovh/ ; https://publer.com/help/en/article/what-are-publers-plans-and-pricing-15h4yqh/ ; https://publer.com/docs/getting-started/rate-limits

**Tracking/no-code (official pricing/docs):**
- Google Sheets/Drive limits: https://support.google.com/drive/answer/37603 ; https://support.google.com/drive/answer/9312312
- Notion: https://www.notion.com/pricing
- Airtable: https://airtable.com/pricing

**Supporting tools (official pricing/docs):**
- Linktree: https://linktr.ee/pricing
- Canva: https://www.canva.com/en_us/pricing/ ; https://www.canva.com/help/manage-uploads/
- CapCut: https://www.capcut.com/help/capcut-standard-vs-pro ; https://www.capcut.com/resource/capcut-standard-vs-pro ; https://www.capcut.com/help/pricing-change ; https://www.capcut.com/help/how-much-does-capcut-pro-cost

**Threads/X (first-party):**
- Threads API posts (limits, 5-link rule): https://developers.facebook.com/docs/threads/posts/
- Threads API overview (rate limits): https://developers.facebook.com/docs/threads/overview/
- Meta newsroom, Threads launch (links allowed): https://about.fb.com/news/2023/07/introducing-threads-new-app-text-sharing/
- X limits (fetched directly): https://help.x.com/en/rules-and-policies/x-limits

**Non-primary, used ONLY as flagged corroboration (not for any factual claim above):**
- WiseChecker Threads new-account restriction analysis (anecdotal): https://wisechecker.com/threads-account-restricted-new-signup/
