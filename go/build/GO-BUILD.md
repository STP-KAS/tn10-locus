Pasting this file is the GO and the lock-in. It may be pasted hours before the start. Do nothing that sends or mines until the times below; then run each line at its time without asking. No further GO will come. If a gate fails, follow the stop rule and log it; do not ask.

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

# GO, the Build side, TN10 storm, Friday 9 Oct 2026

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

Every clock time here is UTC. This file is self-contained. It was written from [PLAN.md](../../plan/PLAN.md), [REHEARSAL-2026-10-09.md](../../plan/REHEARSAL-2026-10-09.md), [MONITOR.md](../../plan/MONITOR.md) and [NEXT-RUN-MONITOR.md](../../plan/NEXT-RUN-MONITOR.md) at the commit that added it. If they disagree on tonight, this file is what you run. The bot's file is [GO-BOT.md](../bot/GO-BOT.md). It uses the same clock.

## 1. Role

You are Grok Build, on stp's desk. You run Build's senders and exactly 1 miner. TN10 only, network `testnet-10`. The Build wallet only. You do not touch the Bot wallet, the bot's runner, or n0. n0 does not run.

## 2. Node

- **locus only**, the first desk kaspad, on the loopback Borsh socket Build already uses for it. UTXO index on.
- Never send to keel, n0, a public node, `bore.pub`, or `159.223.110.159`.
- You may read keel on its desk loopback (read only, no sends) for the rehearsal gate in §5.
- Leave both kaspad processes and stp's tunnel to keel running. They are not yours to stop.
- No host, IP, port, key, seed or txid goes into git or into any result file.

## 3. Miner

- Exactly 1 miner, on locus only. Its own user agent, logged.
- On from 20:30 to 05:00. Off for the miners-off settle and control, 22:00–22:25. The bot turns its miner off at the same times.
- Stop every other desk miner. No desk miner on keel, before or after keel syncs.

## 4. Before 20:15 UTC, prepare only

**Pre-check: the ~10-minute freeze. Write findings, don't block launch.** On 9 Oct keel froze for 3–5 minutes about every 10 minutes from about 14:05, with no bot load and nobody at the desk, while the public node ran about 9.6 DAA per second. Check and write, with times: your own sender steps or restarts, locus or keel pruning or other housekeeping in their logs, Defender scans of the kaspad data folders, Task Scheduler jobs, and anything else on a 10-minute rhythm. Nothing found is written as nothing found. Write it to `tn10-storm-2026-10-09/build/precheck.md`. You may change nothing on the desk for it unless the cause is your own process.

Then:
- **Every Build sender not in this file stops by 20:15** (pre-run fleets, fillers, old lanes), so the rehearsal and B0 see TN10 without them. The 3 Oct halt file on the older fleet stays `halt`. **Not sure / open for debate:** on 9 Oct most of the ~1,600 tx/s outside load on keel was likely the desk's own senders.
- Read locus: synced, UTXO index, mempool, normal fee, RSS, free RAM, desk disk. Send only if synced and the UTXO index is on.
- Desk NTP: `w32tm` against time.windows.com, 5 samples. Repeat at 05:00. A move over 50 ms flags Build's confirmation times.
- Write `steps-utc.json` from the table in §5, same UTC times as the bot. That file is the step clock.
- Start the loggers in §9 now. They run to 05:00.

## 5. Schedule and rates

T0 is **21:00**. End is **Saturday 10 Oct 2026, 05:00**. His counter (Kaspa Pulse) is 21:25–05:35; it does not move T0.

**Rehearsal, 20:30–21:00**, only if keel lag ≤ 60 s at 20:15 and at 20:30 (lag = UTC now − timestamp of keel's sink block). Otherwise write **not run** with the lag and its UTC. Details: [REHEARSAL-2026-10-09.md](../../plan/REHEARSAL-2026-10-09.md). Your part:

| UTC | Rehearsal step | Build | Bot |
|---|---|---|---|
| 20:30–21:00 | miner split | 1 miner on locus; it must find ≥ 1 block. Log mining share on locus. | 1 miner on keel |
| 20:30–20:50 | bot runners, light lane | 0 | sending on keel |
| 20:50–20:53 | bot only | 0 | 60 tx/s |
| 20:53–20:56 | Build only | 60 tx/s | 0 |
| 20:56–20:59 | both | 60 tx/s | 60 tx/s |
| 20:59–21:00 | wrap | 0 | 0 |

**Storm.** "Ours" is the two sides' combined added load. Probes and the ordered stream (§8) are counted by id.

| # | UTC | Phase | Miners | Build on locus | Bot on keel |
|---|---|---|---|---|---|
| 1 | 21:00–21:10 | B0 baseline | on | 0 | 0 |
| 2 | 21:10–21:20 | C1, bot alone | on | 0 | 60 |
| 3 | 21:20–21:30 | C2, Build alone | on | 60 | 0 |
| 4 | 21:30–21:40 | C3, both | on | 60 | 60 |
| 5 | 21:40–21:55, drain to 22:00 | 2× | on | ours − bot | bot level |
| 6 | 22:00–22:05 | settle | **off** | 0 | 0 |
| 7 | 22:05–22:20, drain to 22:25 | 2× miners-off control | **off** | same as row 5 | same as row 5 |
| 8 | 22:25–22:30 | settle | on | 0 | 0 |
| 9 | 22:30–22:45, drain to 22:50 | 5× | on | ours − bot | bot level |
| 10 | 22:50–23:05, drain to 23:10 | 10× | on | ours − bot | bot level |
| 11 | 23:10–23:25, drain to 23:30 | 20× | on | ours − bot | bot level |
| 12 | 23:30–23:45, drain to 23:50 | 30× | on | ours − bot | bot level |
| 13 | 23:50–00:05, drain to 00:15 | max | on | uncapped (§7) | bot level |
| 14 | 00:15–00:25 | B1 baseline | on | 0 | 0 |
| 15 | 00:25–04:45 | long hold | on | Build's last clean rate | last clean bot level |
| 16 | 04:45–05:00 | final drain | on | 0 | 0 |

**"Ours" per step.** From B0, B = median network-wide unique accepted tx/s over 21:00–21:10, minus probe and stream ids.
- If 50 ≤ B ≤ 200: ours = (m − 1) × B at step m×. Rows 5 and 7 are capped at 250 tx/s total network load, and that is written.
- Otherwise (on 9 Oct, B would have been about 1,600): ours = 250 (rows 5 and 7), 1,000 (5×), 1,500 (10×), 2,000 (20×), 2,500 (30×).

**Bot level** starts at 60 tx/s and at most doubles at a step boundary while keel stays clean. You do not see it live. Use this rule for your own target: **Build = ours − 60 at row 5, then ours − 120, − 240, − 480, − 960** for rows 9–12 if you have no word from the bot. Do not raise your target mid-step to cover a bot shortfall. The real bot rates come from the bot's folder after the run.

**Build's clean rate** for the long hold: the highest step where locus did not saturate (§9) and mean submit was ≥ 95% of target with no zero second. If none, 250 tx/s.

**Drains.** Senders 0, miner as the row says, every logger on.

## 6. Gates and stop rules

- **locus.** Synced and UTXO index on, or senders 0 and the row says `down`. Check every 10 minutes.
- **Free RAM under 1 GB, or a dead locus or sender process:** stop Build's senders. Restart at the next step start if RAM is back ≥ 1 GB and locus is synced. Log it.
- **Fee gate.** At every step start read locus's normal quote. If it is above 200, Build sits out that step (`waiting: quote`, write the quote) and reads again at the next step start.
- keel's health is not your gate. If the bot is waiting, keep your schedule.
- Never more senders than §7 allows. Never a second miner. Never auto-scale inside a step, never pause a step for mempool.
- Any other fault: senders 0, log it with UTC, retry at the next step start. Do not ask.

## 7. Senders and fees

- **4 fixed sender processes** on every paced step, each with its own coin set and logs. Depth 2, in-flight 48, four connections each. Target ÷ 4 per process. If they cannot hold the target, the step is **sender-limited**; log it, do not add senders.
- **Max step only:** add one sender at a time, every 2 minutes, while locus stays up and free RAM stays ≥ 1.5 GB. Never more than 9 (ten faulted locus on 8 Oct).
- Ordered stream in its own process: 2 per second per tier at 1× and 1.5×, independent self-transfers from a pre-split pool, in every load row (not B0, B1, settles or drains), inside Build's share.
- **Fees.** Pair 200 and 300 sompi/gram, cap 600, floor 200. Frozen per step from locus's quote: half the lanes at 1× (200), half at 1.5× (300). The pair stays until a multi-hour seen-accepted rate over 2,207 is written in the questions plan. A higher fee reorders inside full blocks; it does not add capacity. Log 1× against 1.5× confirmation per step: n, p50, p95, p99, worst, share over 30 s and over 60 s.

## 8. Not on this side

No light lane on Build tonight. The light tx (P2SH `OP_TRUE`, 637 mass) is the bot's optional lane, labelled **anyone-can-spend hops, not realistic payments**. The bot's runner hop has the same no-signature shape (643 mass). Build's senders are the signed-payment side: their rates are labelled **signed payment** and are the only signed-payment rates besides the probes and stream (§12).

## 9. What to log

**Every second, per sender:** sender id, target, submitted, accepted, endpoint `locus`, locus mempool, submit latency. On a sample and every reject: submit and accept time, UTC with ms and `Z`. Per-transaction logging stays on.
**Every minute, per sender:** minute, sender id, node `locus`, tx_sent, five ids spread across the minute (local only). One combined Build line.
**Every minute, the chain count on locus (§12):** locus `block-added` full blocks against locus's `getVirtualChainFromBlock` `acceptedTransactionIds`: blocks/s, selected-chain blocks/s, tx slots/s, unique ids/s, duplicate share = 1 − unique/slots, unique accepted/s, valid or not (§12), Build's own ids accepted/s, and the same share for Build's own ids. If the reader cannot keep up, fall back to 60 s every 5 minutes and write that as a deviation. If you cannot read it at all, write **not measured** once with the reason.
**Every 10 minutes, the Build row:** UTC, session, sender count, desk disk, `w32tm` (latest), locus synced, UTXO index, mempool, normal fee, RSS, free RAM, desk CPU, Build submitted tx/s and Build accepted tx/s (own ids, attribution only, labelled signed payment), locus unique accepted tx/s (chain count, valid or not), rejects by reason, miner count, mining share on locus (blocks total, ours, %), the six public pools by name, indexer health (`https://api-tn10.kaspa.org/info/health`), keel lag read on the desk, usage (or **not measured**).
**Per step:** saturation on locus (accepted under 95% of submit-OK for 60 consecutive seconds, from 60 s after start): yes or no, onset. Mean submit against target, zero seconds. Plateau label: sender-limited, node-bound, network-bound, unclear.
**Every minute, the miner log and the network line (§13):** Build miner running 0/1, threads, hashrate, blocks we mined, reason for any on/off change; locus blocks/min, tx per block, unique accepted. Required, also while the miner is off.

A required line with no reading is **not measured**, with the UTC it was due.

## 10. End and results

- 04:45 senders 0. 05:00 miner off, loggers stop, desk NTP read again.
- Results go to this repo, folder `tn10-storm-2026-10-09/build/`: README with the step table (Build submitted and accepted as attribution, locus unique accepted with valid minutes, duplicate share network and own), every rate labelled by shape (§12), the per-minute chain-count CSV, precheck findings, gate events, fee tiers, mining share, and the CSV/JSONL data. Counts only. No txid, key, seed, host, IP or port. If you cannot push, leave the folder on the desk and write that in your last message; stp commits it.
- Commit as `STP-KAS <227352643+STP-KAS@users.noreply.github.com>`, push to main. No tags, no releases. The bot writes `COMBINED.md` from both folders by §12: one headline counted once, never locus accepted plus keel accepted. Do not ping Kaspa Pulse.
- Labels on every finding: **Claim (measured on TN10)**, **Not sure / open for debate**, **Needs more testing**.

## 11. Settled before launch (your audit, 9 Oct)

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

**Build's part.**
- Measure on locus every minute: the chain count above (locus's unique accepted, blocks, slots, unique ids in blocks, selected-chain blocks, duplicate share, valid or not with the reason), plus Build's own ids accepted and their duplicate share. locus is the first choice for the headline, so this reading matters most. If you cannot read it, write **not measured** with the reason and keel's count is used.
- Log every Build rate with the label **signed payment**, with the mass of the sender's transaction. If any Build sender uses another shape, label it and keep it apart.
- Put the per-minute chain counts in `tn10-storm-2026-10-09/build/` as CSV, so `COMBINED.md` can pick per minute.

## 13. Miner log and blocks per second (same text in GO-BOT.md and GO-BUILD.md)

Added after Kaspa Pulse's notes of 9 Oct. This section adds logging and reporting only. It does not change any time, step, rate or order in the timeline above, and it does not change when a miner is on or off.

**Why.** Kaspa Pulse, who counts TN10 independently, saw on 9 Oct that blocks per second moved together with throughput: minutes with fewer blocks had fewer accepted tx/s, while transactions per block stayed about the same. That looks like fewer blocks being mined at times, not load pushing blocks down. A per-minute miner log on each side, next to a per-minute network line, lets us say which it is for sure.

**Every minute, the miner log (each side, required).** One row per UTC minute from 20:15 to 05:00, also while the miner is off. Files `miner-1m.jsonl` and `miner-1m.csv` in the side's results folder. Columns:
- `minute_utc` (start of the minute, with `Z`) and `minute_cest`.
- `miners_running`: 0 or 1; 1 only if the side's one miner was up the whole minute. `miner_up_s`: seconds up out of the seconds sampled.
- `threads`: miner threads (0 when off).
- `hashrate`: from the miner's own log, with its unit, or **not measured**.
- Blocks we mined that minute: `blocks_found` and `blocks_submitted_ok` from the miner's own log, and `our_blocks_in_dag` (blocks with our coinbase tag seen by the side's node that minute, from the chain count).
- `change` (on, off, or empty) and `reason` for any on/off change in that minute: plan time, lag gate, tunnel, process exit, operator.

**Every minute, the network line (each side, next to the miner log),** from the side's own chain count (§9, §12): `blocks` added that minute = blocks/min (blocks/s = blocks/min ÷ 60), `tx_per_block` = non-coinbase tx slots ÷ blocks, `unique_accepted` and unique accepted/s, and `valid`. Fewer blocks mined shows as blocks/min down with tx per block steady and a miner off or down. Load pushing blocks down shows as blocks/min down while load rises and both miners are up.

**The direct test is rows 6–8.** Both miners are off 22:00–22:25 UTC (00:00–00:25 CEST), and row 7 carries the same load as row 5. Compare blocks/min, tx per block and unique accepted in row 7 against row 5, with both miner logs showing 0. Write the result with its label (§10).

**The headline is the chain count (§12), never our own submit/accept counter.** On 8 Oct our own mempool-accept counter read a few % below the independent count of transactions in blocks, in every round. Our submitted and accepted numbers stay attribution only.

**Independent count.** Kaspa Pulse's counter starts at 21:25 UTC (23:25 CEST), 25 minutes after T0, so it misses B0 and most of the one-side control (rows 1–3). stp asks him whether he can start at 20:55 UTC (22:55 CEST). This does not move T0 or anything else. Do not ping him (§10); stp sends him the plain-text summary.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
