> **Experimental. We are just trying this.**
>
> [Disclaimer](DISCLAIMER.md)

Thank you, Kaspa Pulse (@gokugalax), for the guidance and the input over this stretch, from 4 Oct 2026 on. The 7 Oct 2026 wording stays: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# tn10-locus: the front door for our TN10 stress tests

Kaspa Testnet-10 (TN10) only. tKAS has no value. Nothing here touches mainnet. Every clock is UTC unless a column says Brussels. No txids, keys, seeds, hosts or IPs are kept in this repo.

## What

This repo is the working hub for the TN10 stress tests run from one desk: two kaspad nodes (**locus** and **keel**), two operators (the Grok **bot** on its box and Grok **Build** on the desk PC), one shared plan, and the measured results. It holds tonight's launch files, the plan, the monitoring results, a map of every related repo, and the [longer history](history/README.md).

## Why

To find out, on a public testnet and with the method written down first, what Kaspa really does when blocks are full. Not a headline TPS number, but the five questions Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) asked:

1. Accepted tx/s vs submitted, over the whole storm, and where acceptance flattens.
2. Confirmation time per load step (median and worst), normal fee vs 1.5×. Does paying more buy inclusion?
3. Does the public indexer freeze, at what sustained tx/s, and for how long?
4. Mempool depth over time: backlog, not just throughput.
5. Does order hold under load? Send order vs accept order.

Plus our own: the highest **unique accepted** tx/s both sides can hold at the same time, and why it sits where it does.

## How

| Piece | What it is |
|---|---|
| **locus** | First kaspad on the desk, testnet-10, UTXO index on. Build sends and mines here only. |
| **keel** | Second kaspad on the desk. The bot sends and mines here only, through a tunnel stp provides. Gate: keel lag ≤ 60 s. |
| **n0** | The old box node. Retired on 8–9 Oct; it does not run. |
| **Bot / Build split** | Each side uses its own wallet and its own node, with exactly 1 miner on its own node ("mine where you send"). |
| **Plan** | [plan/PLAN.md](plan/PLAN.md) is the method; [plan/REHEARSAL-2026-10-09.md](plan/REHEARSAL-2026-10-09.md) is the pre-T0 rehearsal. The questions and method come from [tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions). |
| **GO files** | One self-contained launch file per side. Pasting it is the GO and the lock-in. No further GO. |
| **Monitoring** | Checklists in [plan/MONITOR.md](plan/MONITOR.md) and [plan/NEXT-RUN-MONITOR.md](plan/NEXT-RUN-MONITOR.md): submitted and accepted per second, mempool, lag, fee tiers, indexer, mining share, duplicate share, NTP. |
| **Rules** | Outside the storm and the rehearsal the bot's runner stays off. If a page and a GO file disagree about tonight, the GO file wins. The questions plan stays the source for the questions and the method. |
| **Labels** | **Claim (measured on TN10)**: measured, source file named. **Not sure / open for debate**: our reading, reason it could be wrong given. **Needs more testing**: the settling test is named. |

## Tonight: Friday 9 Oct 2026

| Side | Paste this | Node |
|---|---|---|
| The bot | [go/bot/GO-BOT.md](go/bot/GO-BOT.md) | keel |
| Grok Build | [go/build/GO-BUILD.md](go/build/GO-BUILD.md) | locus |

T0 is 21:00 UTC (23:00 Brussels), 8 hours, ending Saturday 10 Oct 05:00 UTC (07:00 Brussels). No fallback day. For tonight the GO files are what each side runs; the same table is in both.

| UTC | Brussels (CEST, UTC+2) | Bot | Build |
|---|---|---|---|
| before 20:15 | before 22:15 | Prepare only: tunnel from the latest `FOR-TN10-OPS.txt`, coins, scripts, read-only loggers. No sends, no miner. | Prepare only: freeze pre-check, coins, scripts, read-only loggers. No sends of this plan, no miner change. |
| 20:15 | 22:15 | keel health check. Rehearsal go/no-go: keel lag ≤ 60 s. | Stop every sender not in this plan. locus health check. Read keel lag for the same go/no-go. |
| 20:30 | 22:30 | Start 1 miner on keel. Second go/no-go read. | Start 1 miner on locus. Second go/no-go read. |
| 20:30–21:00 | 22:30–23:00 | Rehearsal, only if keel is healthy: 60 tx/s 20:30–20:40, light lane 20 tx/s 20:40–20:45 and 50 tx/s 20:45–20:50 (runners 0), 60 tx/s 20:50–20:53, 0 20:53–20:56, 60 tx/s 20:56–20:59. | Rehearsal, only if keel is healthy: 0 until 20:53, 60 tx/s 20:53–20:59. |
| 21:00–21:10 | 23:00–23:10 | T0. B0 baseline, no load. Miner on. | B0 baseline, no load. Miner on. |
| 21:10–21:20 | 23:10–23:20 | 60 tx/s (bot only) | 0 |
| 21:20–21:30 | 23:20–23:30 | 0 | 60 tx/s (Build only) |
| 21:30–21:40 | 23:30–23:40 | 60 tx/s | 60 tx/s |
| 21:40–21:55, drain to 22:00 | 23:40–23:55, drain to 00:00 | Step 2×, 250 combined: bot level (60) | Step 2×, 250 combined: 250 − 60 = 190 |
| 22:00–22:05 | 00:00–00:05 | Settle, 0. Miner **off**. | Settle, 0. Miner **off**. |
| 22:05–22:20, drain to 22:25 | 00:05–00:20, drain to 00:25 | Miners-off check, same rate as 2×. Miner off. | Miners-off check, same rate as 2×. Miner off. |
| 22:25–22:30 | 00:25–00:30 | Settle, 0. Miner back on. | Settle, 0. Miner back on. |
| 22:30–22:45, drain to 22:50 | 00:30–00:45, drain to 00:50 | Step 1,000 combined: bot level | 1,000 − bot (plan: 880) |
| 22:50–23:05, drain to 23:10 | 00:50–01:05, drain to 01:10 | Step 1,500 combined: bot level | 1,500 − bot (plan: 1,260) |
| 23:10–23:25, drain to 23:30 | 01:10–01:25, drain to 01:30 | Step 2,000 combined: bot level | 2,000 − bot (plan: 1,520) |
| 23:30–23:45, drain to 23:50 | 01:30–01:45, drain to 01:50 | Step 2,500 combined: bot level | 2,500 − bot (plan: 1,540) |
| 23:50–00:05, drain to 00:15 | 01:50–02:05, drain to 02:15 | Max step: bot level | Max step: uncapped, up to 9 senders |
| 00:15–00:25 | 02:15–02:25 | B1 baseline, no load. End of paced steps at 00:25. | B1 baseline, no load. End of paced steps at 00:25. |
| 00:25–04:45 | 02:25–06:45 | Long hold at the last clean bot level (30 if none) | Long hold at Build's last clean rate (250 if none) |
| 04:45–05:00 | 06:45–07:00 | Final drain, senders 0 | Final drain, senders 0 |
| 05:00 | 07:00 | End. Miner off, loggers stop. | End. Miner off, loggers stop. |

Rates are tx/s. **Bot level** starts at 60 and at most doubles at each clean step (60, 120, 240, 480, 960), never above the combined step; if a step is not clean it goes back to the last clean level. "Plan" in the Build column is that doubling path; Build uses it and never raises its target mid-step to cover a bot shortfall. The combined numbers are the fallback, used when B0's baseline B is below 50 or above 200 tx/s (on 9 Oct it was about 1,600). If 50 ≤ B ≤ 200, combined = (m − 1) × B for steps 2×, 5×, 10×, 20×, 30×, with 2× and the miners-off check capped at 250 tx/s total.

Kaspa Pulse counts the chain from outside, on his own clock (Friday 21:25 UTC through Saturday 05:35 UTC, set when T0 was still 21:30). His clock does not move T0. Tonight's results go to `tn10-storm-2026-10-09/` (bot, build, combined) in this repo.

## Results so far

Full pages: [monitoring-result/](monitoring-result/README.md) ([bot, keel](monitoring-result/bot-result/README.md) · [Build, locus](monitoring-result/build-result/README.md)), the reasoning in [goal/README.md](goal/README.md) and [goal/OPINION.md](goal/OPINION.md), and older storms in the [history](history/README.md).

- **Claim (measured on TN10):** a block holds 500,000 compute mass; a signed 1-in/1-out payment is about 1,624 mass, so about 308 per block and about 3,080 tx/s at 10 blocks/s. On 9 Oct blocks held about 300–350 transactions (max 691).
- **Claim (measured on TN10):** on keel, 9 Oct, 48–49% of tx slots in blocks were duplicates of a transaction already in another block (12:29 and 12:55 UTC). Transactions seen only in red (off-chain) blocks were accepted too. The gap is copies, not lost transactions.
- **Claim (measured on TN10):** network unique accepted while keel kept up (12:24–13:15 UTC): average 1,627 tx/s, median 1,704, max 2,435. No valid window held 3,000 unique accepted tx/s.
- **Claim (measured on TN10):** fee tiers 300 vs 200 sompi/gram: 1.5× was about 0.5 s faster at p50 in every step; both tiers landed.
- **Not sure / open for debate:** fees reorder transactions in full blocks; they do not add room. Duplicate share, not block space, is why unique accepted sits near 2,000 instead of 3,080. Mining on your own sender's node may lower it; tonight's one-side control measures that.
- **Needs more testing:** the light (anyone-can-spend, ~637–643 mass) lane at scale; the ~10-minute keel freezes seen from about 14:05 UTC on 9 Oct (cause not found).
- Earlier peaks, for context: box-only best minute 4,253 tx/s on 2 Oct and a 6-hour desk hold of 2,207 seen-accepted tx/s on 6–7 Oct. Those used older setups and a different counter; see the history.

## Credit: Kaspa Pulse

Thank you, Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)), for the guidance and the input over this stretch, from 4 Oct 2026 on. He shaped this test through those notes. He stays out of the setup, counts the chain from outside, and sends his comparison first. In short, he gave us:

- **The five questions** above.
- **Six method points:** write the plan first and publish it with a commit SHA and a deviations list; a 10-minute baseline first; fixed load steps, not one blast; submitted and accepted logged per second in UTC, with send order vs accept order; mining share stated up front; raw data next to the summary.
- **Four tightenings:** a miners-off control in the main run; label each plateau box-bound or network-bound; NTP-synced clocks with offsets logged; saturation defined before T0 (accepted under 95% of submitted for 60 s), with reorder rates as counts and probe n raised.
- **Discipline on numbers:** a stuck pool is named chain or node before anyone calls it a ceiling; "one clean run first", then weekly; the words senders, runner and bot.

Where each point is recorded, with dates, is in [history/README.md#credit-kaspa-pulse-in-full](history/README.md#credit-kaspa-pulse-in-full).

## Map of related repos

All under [STP-KAS](https://github.com/STP-KAS). Private repos are linked for the record; they open only for the owner.

| Repo | What | Period | Status | Link |
|---|---|---|---|---|
| tn10-locus (this repo) | Two-node hub: GO files, plan, 9 Oct monitoring, history | 8 Oct → | Active. **Private** | [link](https://github.com/STP-KAS/tn10-locus) |
| tn10-storm-throughput-questions | Kaspa Pulse's questions, the measurement plan, his notes, raw files from earlier runs | 4 Oct → | Active as the method source; its clock (21:30 UTC) is superseded by tonight's GO files. Public | [link](https://github.com/STP-KAS/tn10-storm-throughput-questions) |
| grok-bot-build-combo | Bot + Build combo hub, 8 Oct checkout (10 desk rounds), Pulse's 8–9 Oct reads | 7–9 Oct | Superseded by this repo for routing; kept as the 8 Oct record. Public (its text says private) | [link](https://github.com/STP-KAS/grok-bot-build-combo) |
| tn10-storm-build-bot-challenge | Where Build and the bot test each other's storm numbers | 6 Oct → | Waiting: empty until the storm | [link](https://github.com/STP-KAS/tn10-storm-build-bot-challenge) |
| tn10-build-desk-tps | Build's desk throughput runs via public nodes, incl. the 6-hour 2,207 hold | 6–7 Oct | Done. Public | [link](https://github.com/STP-KAS/tn10-build-desk-tps) |
| tn10-build-desk-tps-3500 | Desk tries for over 3,500 included tx/s (not reached) and the light-hop idea | 7 Oct | Done. Public | [link](https://github.com/STP-KAS/tn10-build-desk-tps-3500) |
| what-limits-tx-rate | The mass ceiling: why a signed payment stops near 3,080 tx/s | 7 Oct | Reference. Public | [link](https://github.com/STP-KAS/what-limits-tx-rate) |
| tn10-storm-2026-10-public-report | Public report of the 1–3 Oct box storm, plus mainnet-implications note | 1–4 Oct | Done. Public | [link](https://github.com/STP-KAS/tn10-storm-2026-10-public-report) |
| tn10-storm-2026-10-analysis | Raw data and Build analysis of the 1–2 Oct storm | 1–7 Oct | Done. **Private** | [link](https://github.com/STP-KAS/tn10-storm-2026-10-analysis) |
| tn10-stress-tests | Private reports (copy of the 1–2 Oct box report) | 28 Sep–2 Oct | Done. **Private** | [link](https://github.com/STP-KAS/tn10-stress-tests) |
| tn10-gusto-20261002, tn10-gusto-ledger, tn10-full-gusto | "Full gusto" desk spend ramps on public nodes | 1–2 Oct | Done. **Private** | [ramp](https://github.com/STP-KAS/tn10-gusto-20261002) · [ledger](https://github.com/STP-KAS/tn10-gusto-ledger) · [notes](https://github.com/STP-KAS/tn10-full-gusto) |
| tn10-indexer-stall-2026-09 | The api-tn10 indexer stall during the 25 Sep storm (cause unproven) | 25–29 Sep | Done. **Private** | [link](https://github.com/STP-KAS/tn10-indexer-stall-2026-09) |
| tn10-vprogs-stress-findings | 25–26 Sep storm with vprogs and tic-tac-toe; upstream findings | 25–26 Sep | Done. Public | [link](https://github.com/STP-KAS/tn10-vprogs-stress-findings) |
| grok-bot-vprogs-round2 … round6, tn10-vprogs-final-verdict | The Sep storm rounds and the verdict | 25–26 Sep | Done. Public | [round 2](https://github.com/STP-KAS/grok-bot-vprogs-round2) · [verdict](https://github.com/STP-KAS/tn10-vprogs-final-verdict) |
| grok-desk-tn10 | Desk CPU miner setup for TN10 | 27 Sep | Done. **Private** | [link](https://github.com/STP-KAS/grok-desk-tn10) |
| tn10-grok, tn10-hard-test | Early TN10 journal (farm mining stress) and the 14 Sep repo catalog | 14–21 Sep | Done. tn10-grok **private**, tn10-hard-test public | [journal](https://github.com/STP-KAS/tn10-grok) · [catalog](https://github.com/STP-KAS/tn10-hard-test) |

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
