# Build transcript — makefun-roblox-forecast-01

Agent session (Muse, subagent) 2026-11-11 ~22:38–23:10 UTC, inside the
competition window (opened 2026-11-11 06:00 UTC). This file is the faithful
record of the session that built this entry; the formal transcript bundle
for submission is produced by the kit's `makefun bundle` command.

Steps taken:
1. Read https://make.fun and the bounty page
   https://make.fun/bounty/roblox-up-and-coming-forecast-01 ($500, top 20,
   must beat the best house entry, ends 2026-11-13 06:00 UTC); downloaded
   the kit (GET https://make.fun/c/roblox-up-and-coming-forecast-01/kit)
   and read RULES.txt in full (format, log-score rule, floor p=0.0001,
   baseline design, escrow, transcript gate).
2. Analysed the kit history (34 reads, 2026-10-30–2026-11-07, 207 distinct
   games): median rank std 14.8 places; top-10 overlap first->last read
   1/10; climbers go from rank ~55-90 to top 10 in days on player-count
   growth (e.g. Survive Your Ideas 55->1, playing x18). Noted the kit
   history holds no practice-window reads (those live in the public
   archive), so backtests used in-history splits.
3. Built a backtest harness mirroring make.fun scoring exactly and compared
   the house persistence baseline against trend-extrapolation variants on
   two out-of-sample splits (24 reads -> next 10; 14 reads -> next 10).
   Tuned horizon (24/36/48), sigma (4/5/7), unnamed share (0.15/0.20/0.30),
   trend half-life, growth-boost, per-game sigma, horizon mixtures.
4. Wrote main.py (Python 3.13 stdlib only): recency-weighted rank-trend
   extrapolation + log(playing) growth pull, 28-day age-out down-weighting
   from details when present, 24/36/48 h horizon mixture, per-game spread,
   25% unnamed per place, max 100 rows per place, deterministic.
5. Verified the shipped main.py: valid forecast.json (540 rows, sums 0.75
   per place, top10 10 distinct, 30,911 bytes < 1 MB); byte-identical on
   re-runs; backtest scores split A -41.803 (baseline -56.902) and split B
   -39.055 (baseline -42.853).
6. Created this public repo (after the competition opened) and pushed.

No model calls at entry runtime; no network; no secrets used or stored.
