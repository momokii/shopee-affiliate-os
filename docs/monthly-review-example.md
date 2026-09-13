# Monthly review — worked example (FICTIONAL numbers)

Read this once so the P5 prompt's output stops being abstract. Every number below is **invented for teaching** — paste only your real Sheet + dashboard numbers into P5.

## Input (month: September, 12 text posts, 3 tags live)

Posts tab (excerpt):

| post_id | platform | format | template | tag | views |
|---|---|---|---|---|---|
| T008 | th | txt | list3 | th_a1_t008_txt | 4.200 |
| T009 | th | txt | story | th_a1_t009_txt | 900 |
| T010 | x | txt | list3 | x_a1_t010_txt | 300 |

Dashboard copy (Laporan Performa, manual):

| tag | Klik | Pesanan | Komisi Kotor (Rp) | status mix |
|---|---|---|---|---|
| th_a1_t008_txt | 210 | 6 | 48.000 | 2 approved / 4 pending |
| th_a1_t009_txt | 25 | 0 | 0 | — |
| x_a1_t010_txt | 8 | 0 | 0 | — |

## The join (what P5 computes)

| tag | views | clicks | CTR proxy (clicks/views) | orders | commission (approved) | EPC (approved/clicks) |
|---|---|---|---|---|---|---|
| th_a1_t008_txt | 4.200 | 210 | 5,0% | 6 | 16.000 | Rp76 |
| th_a1_t009_txt | 900 | 25 | 2,8% | 0 | 0 | Rp0 |
| x_a1_t010_txt | 300 | 8 | 2,7% | 0 | 0 | Rp0 |

Median views = 900. T008 at 4.200 views = 4,7x median → winner candidate. Top EPC by a mile → confirmed winner.

## Verdicts (what good output looks like)

- **START — `list3` on Threads.** Evidence: 4,7x median views + only tag with approved commission (EPC Rp76). Action: P3 → 10 clones in the same template, new topics; P4 → 1 carousel + 1 video from T008's hook.
- **CONTINUE — `story` on Threads (one more cycle).** Evidence: near-median views, clicks exist (2,8% CTR) but zero orders — possible volume trap, but only 1 data point. Action: hold 2–4 more story posts with a different product category before judging.
- **STOP — Threads→X mirroring for 30 days.** Evidence: 300 views, 8 clicks, Rp0 across the mirror. Action: reallocate X slots to Threads list3 clones; revisit X only after a second Threads winner exists.
- **Next week (max 5):** 1) P3 on T008 → schedule 10 clones; 2) P4 carousel from T008; 3) 3 story posts, new product category; 4) pause X queue; 5) fix: T010's comment went up 6h late — keep ≤60 min.

## Assumptions NOT made (P5 must end with this)

Pending Rp32.000 excluded from EPC (not cash until validated); GMV never quoted as earnings; no rate-table lookup (per-product rates only); X verdict is 30-day pause, not permanent — one tag is not a channel verdict.
