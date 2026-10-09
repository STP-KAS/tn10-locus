Pasting this file is the GO and the lock-in. It may be pasted hours before the start. Do nothing that sends or mines until the times below; then run each line at its time without asking. No further GO will come. If a gate fails, follow the stop rule and log it; do not ask.

Before 20:15 UTC: prepare only (check the tunnel from the latest FOR-TN10-OPS.txt, the coins, the scripts); no sends, no miners.

## Timeline (identical in GO-BOT.md and GO-BUILD.md)

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


> **Experimental. We are just trying this.** [Disclaimer](../../DISCLAIMER.md)

# GO, the bot side, TN10 storm, Friday 9 Oct 2026

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

Every clock time here is UTC. This file is self-contained. It was written from [PLAN.md](../../plan/PLAN.md), [REHEARSAL-2026-10-09.md](../../plan/REHEARSAL-2026-10-09.md), [MONITOR.md](../../plan/MONITOR.md) and [NEXT-RUN-MONITOR.md](../../plan/NEXT-RUN-MONITOR.md) at the commit that added it. If they disagree on tonight, this file is what you run. Build's file is [GO-BUILD.md](../build/GO-BUILD.md). It uses the same clock.

## 1. Role

You are TN10 ops, on the box. You run the bot's runner (the senders) and exactly 1 miner. TN10 only, network `testnet-10`. The Bot wallet only. You do not touch Build's wallet, locus, or n0. n0 does not run.

## 2. Node

- **keel only**, the second kaspad on stp's desk, through the tunnel in the latest desk handoff `FOR-TN10-OPS.txt`: Borsh wRPC from `nodeB_wrpc`, gRPC from `nodeB_grpc`. If no newer handoff has come, use the paid tunnel already in use on 9 Oct for both runners and miner.
- Never invent a host. Never use `ws://127.0.0.1:17310` or `127.0.0.1:16310` from the box (those are keel's desk loopback). Never send to locus, n0, a public node, `bore.pub`, or `159.223.110.159`.
- If the tunnel stops answering: retry for up to 60 seconds, then senders 0 and the row says `waiting: tunnel`. Retry every minute. Resume at half the last clean rate once keel answers and passes the gate in §6.
- No host, IP, port, key, seed or txid goes into git or into any result file.

## 3. Miner

- Exactly 1: box CPU `kaspa-miner`, 1 thread, on keel's gRPC through the tunnel.
- Pays `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`. User agent suffix `stp grok bot`.
- On from 20:30 (rehearsal start, or 20:30 even if the rehearsal is not run) to 05:00, while keel is synced. Off over 300 s keel lag; back on once lag ≤ 60 s.
- Off for the miners-off settle and control, 22:00–22:25. Build turns its miner off at the same times.
- Never on locus. No second miner.

## 4. Before 20:15 UTC, prepare only

- Read keel: `getServerInfo` (testnet-10, synced, UTXO index on), sink timestamp, DAA score, mempool size, fee estimate. **Keel lag** = UTC now − timestamp of keel's sink block.
- Box disk: ≥ 35 GB free, go. 28–35 GB, go with 10-minute steps, written as a deviation. Under 28 GB, the bot does not send; miner and loggers still run.
- Box NTP, 5 samples against two public servers. Repeat at 05:00.
- Bot wallet: spend fresh coinbase and mature UTXOs read in small batches. No spending limit (stp, 9 Oct). Never list all old UTXOs in one call.
- Write `steps-utc.json` from the table in §5, with a UTC start and end for every row. That file is the step clock.
- Start the loggers in §9 now. They run to 05:00.

## 5. Schedule and rates

T0 is **21:00**. End is **Saturday 10 Oct 2026, 05:00**. His counter (Kaspa Pulse) is 21:25–05:35; it does not move T0.

**Rehearsal, 20:30–21:00**, only if keel lag ≤ 60 s at 20:15 and at 20:30. Otherwise write **not run** with the last lag read and its UTC, and wait for 21:00. Details and pass rules: [REHEARSAL-2026-10-09.md](../../plan/REHEARSAL-2026-10-09.md).

| UTC | Rehearsal step | Bot | Build |
|---|---|---|---|
| 20:30–21:00 | 1 keel health + freeze watch; 2 miner split | 1 miner on keel | 1 miner on locus |
| 20:30–20:40 | 3 runners | 60 tx/s | 0 |
| 20:40–20:45 | 4a light lane | light 20 tx/s, runners 0 | 0 |
| 20:45–20:50 | 4b light lane | light 50 tx/s, only if 4a passed | 0 |
| 20:50–20:53 | 5 bot only | 60 tx/s | 0 |
| 20:53–20:56 | 5 Build only | 0 | 60 tx/s |
| 20:56–20:59 | 5 both | 60 tx/s | 60 tx/s |
| 20:59–21:00 | wrap | 0 | 0 |

**Storm.** "Ours" is the two sides' combined added load. Probes and the ordered stream (§8) run in every row and are counted by id.

| # | UTC | Phase | Miners | Bot on keel | Build on locus |
|---|---|---|---|---|---|
| 1 | 21:00–21:10 | B0 baseline | on | 0 | 0 |
| 2 | 21:10–21:20 | C1, bot alone | on | 60 | 0 |
| 3 | 21:20–21:30 | C2, Build alone | on | 0 | 60 |
| 4 | 21:30–21:40 | C3, both | on | 60 | 60 |
| 5 | 21:40–21:55, drain to 22:00 | 2× | on | bot level | ours − bot |
| 6 | 22:00–22:05 | settle | **off** | 0 | 0 |
| 7 | 22:05–22:20, drain to 22:25 | 2× miners-off control | **off** | same as row 5 | same as row 5 |
| 8 | 22:25–22:30 | settle | on | 0 | 0 |
| 9 | 22:30–22:45, drain to 22:50 | 5× | on | bot level | ours − bot |
| 10 | 22:50–23:05, drain to 23:10 | 10× | on | bot level | ours − bot |
| 11 | 23:10–23:25, drain to 23:30 | 20× | on | bot level | ours − bot |
| 12 | 23:30–23:45, drain to 23:50 | 30× | on | bot level | ours − bot |
| 13 | 23:50–00:05, drain to 00:15 | max | on | bot level | uncapped |
| 14 | 00:15–00:25 | B1 baseline | on | 0 | 0 |
| 15 | 00:25–04:45 | long hold | on | last clean bot level | Build's last clean rate |
| 16 | 04:45–05:00 | final drain | on | 0 | 0 |

**"Ours" per step.** From B0, B = median network-wide unique accepted tx/s over 21:00–21:10, minus our probe and stream ids.
- If 50 ≤ B ≤ 200: ours = (m − 1) × B at step m×. Rows 5 and 7 are capped at 250 tx/s total network load, and that is written.
- Otherwise (on 9 Oct, B would have been about 1,600): ours = 250 (rows 5 and 7), 1,000 (5×), 1,500 (10×), 2,000 (20×), 2,500 (30×). Each step is also reported as a multiple of B.

**Bot level.** Start at 60 tx/s (row 5). At each step boundary: if the last step was clean (eventual accept ≥ 99%, p90 submit-to-accept ≤ 10 s, keel lag ≤ 60 s the whole step), the next level is min(2 × last level, ours). If not clean, go back to the last clean level. Nothing changes inside a step except the gate in §6. The bot's part never exceeds ours. Build carries ours − bot.
**Long hold.** The bot holds its last clean level. If none was clean, 30 tx/s, still behind the gate.

**Drains.** Senders 0, miner as the row says, every logger on.

## 6. Gates and stop rules

- **Keel health gate.** Send only while keel is synced and lag ≤ 60 s. Lag > 120 s: halve the rate. Lag > 300 s: senders 0 and miner off. Resume at half the last rate once lag ≤ 60 s, then follow the bot level rule at the next step boundary. The row says `waiting` with the lag. A waiting minute adds 0 and is not a failed match.
- **Freeze.** keel's DAA score not moving for ≥ 60 s while the public node's moves. Log start, length and keel lag. Treat it through the gate. On 9 Oct keel froze 3–5 minutes about every 10 minutes from about 14:05.
- **Fee gate.** At every step start, read keel's normal quote. If it is above 200, the bot sits out that step (`waiting: quote`, write the quote) and reads again at the next step start.
- **Disk.** Box under 28 GB: senders 0 for the rest of the run.
- **Never** restart the storm early, add a node, add a miner, or exceed 15 runners.
- Any other fault: senders 0, log it with UTC, retry at the next step start. Do not ask.

## 7. Runners and fees

- **15 runners**, 4 wRPC connections each, depth 2, rate split evenly. stp raised the cap from 6 to 15 in chat on 9 Oct (11:15–11:23); 15 ran on keel at under 10% CPU each. This is a deviation from the questions plan's "6, a 7th on max, never 8", written with that time and reason. Never 8 still holds for any box runner not on keel.
- Hop: the 9 Oct lane hop (1 in, 1 out, P2SH `OP_TRUE`, 643 mass, no signature). Each runner spends its own coins. Every runner rate carries the label **no-signature hop, anyone-can-spend, not realistic payments**; it is never reported as a signed-payment rate (§12).
- **Fees.** Pair 200 and 300 sompi/gram, cap 600, floor 200. Frozen per step from keel's quote: even lanes 1× (200), odd lanes 1.5× (300). The pair stays 200/300 until a multi-hour seen-accepted rate over 2,207 is written in the questions plan. **Claim (measured on TN10):** on 9 Oct, 1.5× beat 1× by about 0.5 s at p50. A higher fee reorders inside full blocks. It does not add capacity.
- Log 1× against 1.5× confirmation per step: n, p50, p95, p99, worst, share over 30 s and over 60 s.

## 8. Light lane (optional)

Only if the rehearsal's step 4 passed and keel passes the gate. P2SH redeem script `OP_TRUE`, 1 in, 1 out, unsigned, 637 mass, small amounts from a pre-split fund. Run it inside the bot level (not on top), at most the rate that passed in the rehearsal (20 or 50 tx/s), in rows 9–12 and 15. Every number from it carries the label **anyone-can-spend hops, not realistic payments**, in its own column apart from the runner hop. If the rehearsal did not run or step 4 failed, the lane stays off and that is written.

**Probes and stream (all rows, 21:00–00:25 and the hold):** one small signed self-transfer per tier (1×, 1.2×, 1.5×, 2× of the frozen quote) every 2 s, and the ordered stream at 2 per second per tier at 1× and 1.5×, from pre-split pools. They go to keel and follow the gate.

## 9. What to log

**Every second, per sender:** sender id, target, submitted, accepted, endpoint `keel`, keel mempool, submit latency. On a sample and every reject: submit and accept time, UTC with ms and `Z`. Per-transaction logging stays on.
**Every second:** keel mempool. **Every 10 s:** keel fee estimate, synced, sink lag, DAA score.
**Every 30 s:** `GET https://api-tn10.kaspa.org/info/health` (cache bypassed): HTTP, `isSynced`, `acceptedTxBlockTimeDiff`, `blueScoreDiff`. Once a minute, one accepted id polled until visible (give up after 30 min).
**Every minute, per sender:** minute, sender id, node `keel`, tx_sent, five ids spread across the minute (local only). One combined bot line.
**Every minute:** keel DAA per second next to the public node's DAA per second.
**Every minute, the chain count (§12):** keel `block-added` full blocks against keel's `getVirtualChainFromBlock` `acceptedTransactionIds`. If the reader cannot keep up or slows the runners, fall back to 60 s every 5 minutes and write that as a deviation with its UTC. Write blocks/s, selected-chain blocks/s, tx slots/s (non-coinbase, summed over blocks), unique ids/s, duplicate share = 1 − unique/slots, unique accepted/s, valid or not (§12), red-only ids accepted, our block share, the bot's own ids accepted/s, and the same duplicate share for our own ids only. A window where keel accepted under 95% of its unique ids is keel lag, not network data. Also one reading per step.
**Every 10 minutes, the bot block:** UTC, session (up, down, waiting), runner count, box disk, NTP, keel synced, lag, mempool, CPU (or **not measured**), bot submitted tx/s and bot accepted tx/s (own ids, attribution only, labelled no-signature), keel unique accepted tx/s (chain count, valid or not), rejects by reason, miner count, mining share on keel (blocks total, ours, %), keel and public DAA/s, freezes since the last block, duplicate share, light lane on or off, usage (or **not measured**).
**Per step:** saturation (accepted under 95% of submit-OK for 60 consecutive seconds, from 60 s after start): yes or no, onset. Clean or not by the bot level rule. Plateau label: sender-limited, node-bound, network-bound, unclear.

A required line with no reading is **not measured**, with the UTC it was due.

## 10. End and results

- 04:45 senders 0. 05:00 miner off, loggers stop, box NTP read again.
- Results go to this repo, folder `tn10-storm-2026-10-09/bot/`: README with the step table (bot submitted and accepted as attribution, keel unique accepted with valid minutes, clean, saturation, duplicate share network and own, mining share), every rate labelled by shape (§12), rehearsal result, gate events, freezes, fee tiers, light lane if run, and the CSV/JSONL data. Counts only. No txid, key, seed, host, IP or port.
- After Build's folder `tn10-storm-2026-10-09/build/` is in, write `tn10-storm-2026-10-09/COMBINED.md` by §12: per minute and per step, the headline network unique accepted tx/s (counted once, from locus if valid, else keel, never the sum of the two), the cross-check, duplicate share, and attribution (bot ids, Build ids, probes and stream, outside), split by shape. The success criteria in §12 are answered at the top. Build cells not in its folder are **not measured**.
- Commit as `STP-KAS <227352643+STP-KAS@users.noreply.github.com>`, push to main. No tags, no releases. Do not ping Kaspa Pulse. The ids for him stay private.
- Labels on every finding: **Claim (measured on TN10)**, **Not sure / open for debate**, **Needs more testing**.

## 11. Settled before launch (Build's audit, 9 Oct)

- **Claim (measured on TN10):** the gap between tx slots and accepted is duplicates across parallel blocks (48–49% of slots at 12:29 and 12:55), not off-chain loss. Transactions only in red blocks were accepted. Report `94929a9`.
- Keep 200/300 unless the quote is above 200.
- No filler aimed at 3,100 tx/s. The steps find where acceptance flattens.
- The one-side control (rows 2–4) runs before the ramp.
- The light tx is labelled anyone-can-spend.
- The headline is network unique accepted tx/s counted once from chain data, not locus accepted plus keel accepted (goal/OPINION.md). Per-side counts are attribution. Rates are split signed payment against no-signature hop (§12).
- Cutting miners is not tonight's change. Tonight's change is one miner per side, on its own node. **Not sure / open for debate** whether it lowers the duplicate share; **Needs more testing**.

## 12. Goal and scoring (same text in GO-BOT.md and GO-BUILD.md)

From [goal/README.md](../../goal/README.md) and [goal/OPINION.md](../../goal/OPINION.md). This section changes how the run is counted and reported. It does not change any time, step, rate or order in the timeline above.

**The headline is one number: network unique accepted tx/s, counted once, from chain data on one synced node.** Each accepted transaction id counts once per minute, when the virtual chain accepts it (`getVirtualChainFromBlock` `acceptedTransactionIds`, or the virtual-chain notification). locus and keel are two views of one chain. **Never add locus's accepted count to keel's.** That counts the same ids twice.

- **Which node counts a minute.** A minute is valid on a node if the node is synced, its lag (UTC now − sink timestamp) is ≤ 60 s the whole minute, and it accepted ≥ 95% of the unique ids it saw in blocks that minute. Headline for the minute = locus's count if locus is valid, else keel's count if keel is valid, else **not measured**. When both are valid, keel's count is written next to it as a cross-check, with the difference. Never the sum, never the mean.
- **Per step.** Headline = median of the valid minutes in the step's load window (drains excluded), with the number of valid minutes. Under 5 valid minutes: **not enough data**.
- **Beside the headline, every minute:** blocks added, tx slots in blocks (non-coinbase, summed over blocks), unique ids in blocks, selected-chain blocks, duplicate share = 1 − unique ids in blocks / tx slots. Slots are never reported as tx/s; a full block of copies is not a higher TPS.
- **Attribution only.** Each side's submitted and accepted are its own ids (Bot wallet, Build wallet; the two never share an id). They say who carried what. They are not added up to make the headline. "Ours accepted" = bot ids accepted + Build ids accepted, each id once; "outside" = headline − ours − probe and stream ids.
- **Transaction shape, labelled separately.** Every rate is split by shape:
  - **Signed payment:** Build's senders, the probes and the ordered stream (1 in, 1 out, signed, about 1,624 mass). Only these are signed-payment rates.
  - **No-signature hop, anyone-can-spend, not realistic payments:** the bot's runner hop (P2SH `OP_TRUE`, 643 mass) and the bot's optional light lane (637 mass). On 9 Oct all bot load already had this shape, so none of the 9 Oct bot rates are signed-payment rates.
  - **Outside load:** shape not known; written as unknown.
  A signed-payment number is never quoted from a mixed total.
- **Success criteria.**
  1. **Goal line:** network unique accepted ≥ 3,000 tx/s as a step median (≥ 10 valid minutes), written with its shape split. A single minute over 3,000 is reported as a peak, not as the goal.
  2. **Signed-payment line:** about 3,080 tx/s (500,000 / 1,624 ≈ 308 per block × about 10 blocks/s). Tonight's signed share (Build plus probes and stream) is planned well under that, so tonight cannot show whether signed payments reach 3,080; write that, do not infer it from the total. 3,500 signed payments do not fit in a block's mass and are not a target.
  3. **Flattening:** the first step where the headline rises by less than half of the rise in ours offered against the previous step. Write the step and both deltas.
  4. **Duplicate share:** network and own-ids, per step. Compare the one-side control (rows 2–4) with the ramp (rows 9–12). Whether one miner per side lowers it stays **Needs more testing** unless the gap is clear in valid minutes.
  5. **Clean:** each side's own eventual accept ≥ 99% per step, as its own rules say.
- **What each side optimizes,** inside the rates above: distinct accepted ids, not submits. Each id goes to one node, once. A higher fee reorders inside full blocks; it does not add room. Submitting faster than the accepted rate fills the mempool and does not move the chain rate.
- Write the minute in UTC. A blank minute is **not measured**. No host, IP, port, address, key, seed or txid in any result file.

**The bot's part.**
- Measure on keel every minute: the chain count above (keel's unique accepted, blocks, slots, unique ids in blocks, selected-chain blocks, duplicate share, valid or not with the reason), plus the bot's own ids accepted and their duplicate share.
- Log every bot rate with the label **no-signature hop, anyone-can-spend, not realistic payments**; the light lane gets its own column under the same label. Probe and stream ids are signed and counted apart.
- Write `COMBINED.md` by the rules above (§10).

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
