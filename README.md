> **Experimental. We are just trying this.**
>
> [Disclaimer](DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Two nodes

Private note. Kaspa Testnet-10 only. Every clock time in this repo is UTC. A clock is not written in local time.

**Goal.** The highest included tx/s the two sides can hold at the same time. Submitted and accepted stay two numbers. The score is accepted. How a block gets past 3,000 included payments, and why a second runner does not double it, is [goal/README.md](goal/README.md). That page does not start the storm and does not move T0.

**Launch tonight.** Paste [plan/GO-BOT.md](plan/GO-BOT.md) into the bot and [plan/GO-BUILD.md](plan/GO-BUILD.md) into Grok Build. Pasting is the GO for that side. Each file is self-contained: node, miner, UTC schedule, rates, gates, logs, results.

**Start.** Sending this GitHub to Grok Build or to the bot means go: start the operation. The same sentence is the forward rule in [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) `TWO-NODES.md`.

**Who sends where.**

| Who | Wallet | Node | When |
|---|---|---|---|
| The bot's runner | Bot only | keel, the second kaspad on the desk | Only during the storm and the rehearsal, and only while keel is synced and its tip lag is at or under 60 seconds. Exactly 1 bot miner, on keel |
| Grok Build, on the desk | Build only | locus, the first desk kaspad | While locus is synced and its UTXO index is on. Exactly 1 Build miner, on locus |

Each side mines where it sends (stp, 9 Oct 2026, 16:06 UTC). No desk miner on keel. No bot miner on locus. Why, and the one-side control, are in [plan/PLAN.md](plan/PLAN.md) §2a and §3b. The 30-minute rehearsal before T0 is [plan/REHEARSAL-2026-10-09.md](plan/REHEARSAL-2026-10-09.md).

Outside the storm and the rehearsal the bot's runner stays off. While keel is still syncing, that runner stays off and Build keeps sending on locus. That minute's combined rate is Build's rate alone.

This page does not lock the questions plan.

## Where this comes from

| Record | What it still is |
|---|---|
| [STP-KAS/tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions) | The questions, the Friday clock, the fee pair, and the raw files from earlier runs. |
| [plan/NEXT-RUN-MONITOR.md](plan/NEXT-RUN-MONITOR.md) | The checklist for the next run. Every line already in the plan. A blank required line fails the pass. |
| [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) | The private combo hub and the 8 Oct checkout sheet. |

## Plan and result

The plan and the result are separate. Both stay.

| Page | What it is |
|---|---|
| [plan/](plan/PLAN.md) | The plan. What to measure, the clock, the fees, and tonight's pastes [GO-BOT.md](plan/GO-BOT.md) and [GO-BUILD.md](plan/GO-BUILD.md). The checklist is [MONITOR.md](plan/MONITOR.md) and [NEXT-RUN-MONITOR.md](plan/NEXT-RUN-MONITOR.md). |
| [monitoring-result/](monitoring-result/README.md) | The result. What was measured. Bot and Build each have their own folder. |

## Monitoring results

Two results. They are not the same number, and they are not added together on the bot's page.

| Side | Who measured | Node | Where the results are |
|---|---|---|---|
| Bot | The box, through the tunnel | keel | [monitoring-result/bot-result](monitoring-result/bot-result/README.md). Final after 15:30 UTC on 9 Oct 2026. Submit, accept, mempool, lag, and miner share in that folder are the bot's. A combined row there is the bot alone. |
| Build | The desk | locus | [monitoring-result/build-result](monitoring-result/build-result/README.md). The 8 Oct desk sheet is linked from that page. |

The heading "Build's view, checked" inside the bot folder is the bot answering a Build claim about mass and off-chain blocks. It is not Build's monitor sheet.

An earlier commit of this repo sent both sides to locus. That routing stays withdrawn. Build stays on locus. The bot uses keel. n0 will not run. The clock, the fee pair, and "never eight box runners" stay.

If this repo and `plan/NEXT-STORM-PLAN.md` disagree about a clock, a fee, or one of Kaspa Pulse's questions, the questions plan wins. If they disagree about which node a side uses, this repo wins.

## The two nodes

**locus** is the first kaspad on this desk. Network `testnet-10`, UTXO index on. It is not a public DNS name. Build reaches it on loopback Borsh. The node cell is `locus`.

**keel** is the second kaspad on this desk. Same network, UTXO index on. It is not a public DNS name. The handoff still writes `node=desk-nodeB`. New logs use `keel`. On the desk its own sockets are Borsh `ws://127.0.0.1:17310` and gRPC `127.0.0.1:16310`. The bot does not use those loopback addresses. The bot's runner and the bot's one miner use the tunnel stp provides. The runner uses the tunnel's Borsh `ws://` address, only during the storm and the rehearsal, and only while keel is synced and passes the plan's keel health gate. The bot's one miner uses the tunnel's gRPC host and port, pays the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`, and mines only while keel is synced. Until the handoff lists the tunnel, both wait. Do not invent a host.

**keel is already in the score.** Read at 2026-10-09T07:59:26Z: block download 69%, last block 2026-10-08T17:03:33Z, not synced, tunnels closed. Those minutes contribute 0 from keel and the row says `waiting`. The combined rate is locus alone. Build's one miner stays on locus, also after keel syncs.

**n0 will not run.** It is the box kaspad. Do not start it, resync it, or keep disk aside for its pruning. The questions plan's older §6a and §9 sentences about n0 are the record of that machine. They are not this operation.

`bore.pub` and `159.223.110.159` stay closed.

## Pastes and the sheet

| Who | Paste | Where it sends |
|---|---|---|
| Grok Build, tonight | [plan/GO-BUILD.md](plan/GO-BUILD.md) | locus |
| The bot, tonight | [plan/GO-BOT.md](plan/GO-BOT.md) | keel |
| Grok Build, standing | [plan/PROMPT-BUILD.md](plan/PROMPT-BUILD.md) | locus |
| The bot's runner, standing | [plan/PROMPT-BOT.md](plan/PROMPT-BOT.md) | keel, only during the storm |

The plan is [plan/PLAN.md](plan/PLAN.md). The monitoring tasks are [plan/MONITOR.md](plan/MONITOR.md). If a paste and the plan disagree, the plan wins.

## Clock

This evening only. No fallback day.

T0 is Friday 9 Oct 2026, 21:00 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:00 UTC. The old Monday 13 Oct line is dropped.

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

The rest of each side's rules are in the two GO files.


Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. It does not move T0.

Pasting a GO file is the storm GO for that side. Each side writes `steps-utc.json` from its GO file's table. The runner runs only during the storm and the rehearsal.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
