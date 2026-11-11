# make.fun — Predict Roblox's Up-and-Coming top 10

Entry for https://make.fun/bounty/roblox-up-and-coming-forecast-01 ($500,
top 20, must beat the best house entry). `main.py` (Python 3.13, standard
library only) reads `/input/history.ndjson` + `/input/task.json` and writes
`/output/forecast.json`.

Method: recency-weighted rank-trend extrapolation per game (48 h half-life),
pulled by log(player-count) growth as a leading indicator; 28-day age-out
down-weighting from game details when present; a 24/36/48 h horizon mixture;
per-game spread from rank scatter around trend; 25% of each place left
unnamed for games never seen before. No network, no model calls,
deterministic (identical bytes on re-runs).

Backtested on two out-of-sample splits of the kit's own history with
make.fun's exact log-score rule: split A -41.80 vs house persistence
baseline -56.90; split B -39.06 vs baseline -42.85.

License: MIT.
