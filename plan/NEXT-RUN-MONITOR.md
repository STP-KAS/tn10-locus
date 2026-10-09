> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Next run monitor

This page lists the monitor lines already written in [MONITOR.md](MONITOR.md) and in [NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md). It does not add a demand. It does not lock the questions plan.

**Start.** Sending this GitHub to Grok Build or to the bot means go: start the operation. The bot's runner and the bot's miners use the tunnel to keel. The runner runs only during the storm. The miners pay the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx` and mine only while keel is synced. n0 will not run.

If this page and the questions plan disagree, the plan wins. If they disagree on which node a side uses, [PLAN.md](PLAN.md) wins.

The next run is Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC. The hours after 00:25 UTC stay unnamed until the storm GO chooses. His counter is 21:25 UTC through 05:35 UTC. It does not move T0.

A required line with no reading is **not measured**. That fails the pass in [MONITOR.md](MONITOR.md). Do not invent the other side. Do not ping Kaspa Pulse. Do not send him the sheet. No key, no seed, and no txid in git. The mining address is the Grok Bot address named above.

The printable copy is `plan/next-run-monitor.pdf` in this repo. If the PDF and this page disagree, this page wins.

## What 8 Oct left unread

The desk rows are in the combo repo, `tonight-8-oct/RESULTS.md`, commit `593a4ba`. The checkout note is the questions repo, `plan/AFTER-8-OCT.md`, commit `ee2ecc1`. These lines were not read. The next run reads each one.

| Line | 8 Oct |
|---|---|
| Bot block on every 10-minute row | Not printed. Every bot cell is **not measured**. |
| Rows 18:00 and 18:10 UTC | Not read. |
| Usage, both sides | **not measured**. |
| n0 synced, lag, mempool, CPU | Not read. |
| Box disk, box NTP | Not read. |
| Desk NTP at 18:00 and at 20:00 as a pair | The 18:00 row and the exact 20:00 pair were not both read. The 50 ms flag was not scored. |
| Per-minute tx sent, node name, five tx ids | Evening locus rounds turned per-transaction logging off. The 18:30 sample was skipped. |
| Indexer every 30 seconds, and one visibility poll | One health sample on the 10-minute row. No freeze by the written rule. |
| n0 mempool every second, fee every 10 seconds | Spot reads about every 10 minutes. |
| Confirmation time, 1× against 1.5× | **not measured**. |
| Ordered stream, send order against accept order | Off. **not measured**. |
| Saturation on n0, 60 seconds under 95% | **not measured**. n0 was not read. |
| Mining share, per node, per step | **not measured**. |
| Miners-off control at the 2× load | Left for this next run. |
| Combined accepted tx/s | Missing the bot side. Locus accept is not the combined rate. |

n0's three unread lines above are closed on 9 Oct 2026. n0 will not run, so the next run does not read it, and those lines are not a failed pass. The next run reads keel instead: synced, lag, mempool, CPU, and mempool every second. Saturation is scored on keel for the bot and on locus for Build.

## Before T0

Stop unless this GitHub has been sent to Grok Build or to the bot, and `steps-utc.json` is in hand, and the clock is at or after the first time in that file. That send is the storm GO. The runner runs only during the storm.

| Check | Owner | Pass |
|---|---|---|
| keel still syncing | Desk | Watch the block download. Leave the tunnel closed. When keel is synced, open the tunnel and write `nodeB_wrpc` and `nodeB_grpc` in the handoff. Say both addresses. That report is not the storm GO. Until then the bot row says `waiting`. |
| keel synced, tip lag seconds, mempool, box disk | Bot | The runner runs only during the storm. Send only if keel is synced and lag is at or under 300 seconds, and the disk gate in the plan passes. Otherwise sender count 0 and the row says `waiting`. |
| keel tunnel for the bot | stp | stp provides the tunnel when keel is synced. Until that tunnel is in the handoff, the bot's runner and the bot's miners wait. From the box, do not use `127.0.0.1`. Do not invent a host. |
| Locus synced, UTXO index, mempool, normal fee, free RAM, desk disk | Build | Send only on loopback Borsh. Free RAM under 1 GB, or a dead process, stops Build. |
| NTP, five samples, both machines | Each side | Desk: `w32tm` against time.windows.com. Box: two public servers. Repeat at the end. A desk move over 50 ms flags Build's confirmation times. |
| Older fleet halt file | Build | First line still `halt`. |
| Quote | Each side, from its own node | If the normal quote is already above 200, that side does not start. |

## Every 10 minutes, both sides

The desk writes the sheet. The box prints its block. Copy the block. A missing block stays **not measured**.

| Field | Bot, keel | Build, locus |
|---|---|---|
| UTC | row time | row time |
| Session | up, down, or waiting | up or down |
| Sender count | lane runners, or 0 while waiting | Build senders |
| Disk free | box GB | desk GB |
| Clock | NTP offset | `w32tm`, 5 samples at start and end; the row can cite the latest |
| Usage | product counter, or **not measured** | product counter, or **not measured** |
| Node | synced, lag seconds, mempool, CPU | synced, UTXO index, mempool, normal fee, free RAM |
| Rates | submitted tx/s and accepted tx/s | submitted tx/s and accepted tx/s |
| Combined | sum of the two submitted rates, and sum of the two accepted rates | same two sums |
| Pools | keel mempool | locus mempool, plus the six public names, each named |
| Indexer | the latest 30-second sample | same check if the box row is missing |
| Miners | bot miners, through the keel tunnel, or off while keel is syncing | desk miners, still on locus until keel is synced |

While the bot's runner is waiting, the combined accepted rate for that minute is Build's rate alone, and the row says so.

## Every UTC second, per sender

One line: sender id, target, submitted, accepted, endpoint `keel` or `locus`, that node's mempool, submit latency. Accept time is when that side's own node reports the transaction.

Per-transaction logging stays on. The 8 Oct high-rate rounds turned it off. This run does not.

On a sample of transactions, and on every reject: submit time and accept time, UTC, with milliseconds and `Z`.

## Every UTC minute, per sender

On top of the second log.

| Field | What it is |
|---|---|
| minute | `YYYY-MM-DDTHH:MM:00Z` |
| sender id | that sender |
| node | `keel` or `locus`. Not the word "public". |
| tx_sent | submissions by that sender in that minute |
| tx ids | five, spread across the minute, not the first five |

One combined line for the same minute: both submitted sums, both accepted sums. The five ids stay in the local log. Git gets the count of ids saved, not the ids. His accepted count is his.

## His five questions

Each one already has a plan section. The next run produces the reading.

| # | Question | Where it is logged |
|---|---|---|
| 1 | Accepted tx/s against submitted, and where acceptance flattens | Per second, both sides, by fee tier. Saturation: from 60 seconds after the step start, accepted under 95% of submit-OK for 60 consecutive seconds. Report yes or no, and the onset. The chain rule uses keel for the bot's runner. A waiting runner is not a zero-second failure. |
| 2 | Confirmation time, median and worst, 1× against 1.5× | Per transaction: sequence, submit time, accept time, fee tier. Probes about 450 per tier per step. Report n, p50, p95, p99, worst, and the share over 30 seconds and over 60 seconds. |
| 3 | Indexer freeze, at what sustained tx/s, and for how long | `GET https://api-tn10.kaspa.org/info/health` every 30 seconds. Log HTTP, `isSynced`, `acceptedTxBlockTimeDiff`, `blueScoreDiff`. Freeze: 3 samples of 503 or timeout, or lag above 120 seconds and rising, or a visibility delay above 300 seconds. One already-accepted id polled once a minute until it is visible. Give up after 30 minutes. The id stays local. |
| 4 | Mempool depth over time | keel mempool every 1 second. Fee estimate every 10 seconds. Locus mempool on the per-second line. The six public names on the 10-minute row. |
| 5 | Whether order holds under load | Ordered stream, 2 per second at 1× and at 1.5×. Reorder rate, out-of-order accepts, stalls, and fee-driven overtakes, each as a count and a percentage, with n and a 95% interval. |

The two headlines stay order under load, and whether 1.5× fee buys inclusion while 1× waits.

The other 95% rule is separate. The Build gate is mean submit at least 95% of that side's target, with no zero second on a sender that was armed. Sender-limited means submit-OK stayed under 95% of target. Report it. Do not call it a network ceiling.

## Also on this run

These are already in the plan. They were not part of the 8 Oct desk rows.

- B0 is 10 minutes. Lane senders off. The plan keeps the box probes and the ordered stream on in B0. Build sends nothing in B0.
- Steps stay 2×, 5×, 10×, 20×, 30×, then max. Nothing changes inside a step. Never eight box runners.
- Miners-off control at the 2× load, matched to the same load with miners on. The control is imperfect. Other miners still change templates. Say that next to the pair. The miners-off share should read about 0% of our own blocks.
- When accepted flattens, log keel CPU, mempool-cap hits, and reject reasons. Label the plateau by the plan's §6a. The questions plan's about 100,000 cap on n0 does not apply to locus or to keel.
- Mining share per node, per step: blocks total, blocks ours, percent. The bot's miners use the keel tunnel and pay the Grok Bot address. Desk miners stay on locus while keel is syncing.
- At T0, cite the SHA of the last commit that changed `plan/NEXT-STORM-PLAN.md`. A deviation gets a time and a reason.
- Raw files next to the summary stay the plan's §8 list. They are not written by this page.

## Pass

The run does not claim the combined goal unless every line in Task 10 of [MONITOR.md](MONITOR.md) is present, and every row in the table "What 8 Oct left unread" has a reading or a written **not measured** with the UTC it was due. The three n0 rows in that table are closed. They do not fail the pass.

Kaspa Pulse counts the chain from outside the setup. Comparison comes to us first.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
