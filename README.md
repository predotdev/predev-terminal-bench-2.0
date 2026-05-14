<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logo-dark.png">
    <img src="logo.png" alt="pre.dev" width="240">
  </picture>
</p>

# pre.dev — Terminal-Bench 2.0 Trajectories

Open trial data for the pre.dev results reported on
[pre.dev/benchmark](https://pre.dev/benchmark).

## Headline

pre.dev + **Haiku 4.5** beats Claude Code + **Sonnet 4.5** by 3.4 points.
pre.dev + **Sonnet 4.6** beats Claude Code + **Opus 4.5** by 2.3 points.
Same harness, same 89 tasks, single trial, no cherry-picking.

## Methodology

- Benchmark: [Terminal-Bench 2.0](https://www.tbench.ai/leaderboard/terminal-bench/2.0) (89 tasks)
- Harness: [`harbor`](https://www.harborframework.com/)
- Method: `pass@1`, single trial per task
- Each task directory contains the full ATIF `trajectory.json`, `result.json`,
  `reward.txt`, and verifier output as produced by `harbor`.
- Claude Code comparison numbers are the chronologically-first trial of
  Claude Code's public 5-trial submissions to the Terminal-Bench leaderboard
  (statistically equivalent single-trial `pass@1`, derived purely from public data).

## Runs

| Directory | Model | Pass | Rate |
|---|---|---:|---:|
| `predev-haiku-4-5__41.6/` | Claude Haiku 4.5 | 37 / 89 | **41.6%** |
| `predev-sonnet-4-6__56.2/` | Claude Sonnet 4.6 | 50 / 89 | **56.2%** |

## Head-to-head vs Claude Code (leaderboard slot-1, pass@1)

| Model tier | Claude Code | pre.dev | Δ |
|---|---:|---:|---:|
| Haiku 4.5 | 24 / 89 = 27.0% | **37 / 89 = 41.6%** | **+14.6 pts** |
| Sonnet 4.5 → Sonnet 4.6 | 34 / 89 = 38.2% | **50 / 89 = 56.2%** | **+18.0 pts** |
| Opus 4.5 vs Sonnet 4.6 *(tier-skip)* | 48 / 89 = 53.9% | **50 / 89 = 56.2%** | **+2.3 pts** |
| Sonnet 4.5 vs Haiku 4.5 *(tier-skip)* | 34 / 89 = 38.2% | **37 / 89 = 41.6%** | **+3.4 pts** |

pre.dev beats Claude Code at every matched-model tier and **skips up a tier**
twice: pre.dev's Haiku result beats Claude Code's Sonnet; pre.dev's Sonnet
result beats Claude Code's Opus.

## Reproducing the pass count

```
find <run-dir>/jobs -name reward.txt -exec cat {} \; | awk '{s+=$1} END {print s}'
```

The Claude Code slot-1 numbers can be reproduced by scraping
[tbench.ai/leaderboard/terminal-bench/2.0/claude-code](https://www.tbench.ai/leaderboard/terminal-bench/2.0/claude-code)
— see `predev-bench/scripts/scrape_tbench_cc.py`.
