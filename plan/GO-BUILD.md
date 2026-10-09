Pasting this file is the GO. Launch at the times below without asking. If a gate fails, follow the stop rule and log it; do not ask.

> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md)

# GO, the Build side, TN10 storm, Friday 9 Oct 2026

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

Every clock time here is UTC. This file is self-contained. It was written from [PLAN.md](PLAN.md), [REHEARSAL-2026-10-09.md](REHEARSAL-2026-10-09.md), [MONITOR.md](MONITOR.md) and [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md) at the commit that added it. If they disagree on tonight, this file is what you run. The bot's file is [GO-BOT.md](GO-BOT.md). It uses the same clock.

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

## 4. Before launch, at once

**Pre-check: the ~10-minute freeze. Write findings, don't block launch.** On 9 Oct keel froze for 3–5 minutes about every 10 minutes from about 14:05, with no bot load and nobody at the desk, while the public node ran about 9.6 DAA per second. Check and write, with times: your own sender steps or restarts, locus or keel pruning or other housekeeping in their logs, Defender scans of the kaspad data folders, Task Scheduler jobs, and anything else on a 10-minute rhythm. Nothing found is written as nothing found. Write it to `tn10-storm-2026-10-09/build/precheck.md`. You may change nothing on the desk for it unless the cause is your own process.

Then:
- **Every Build sender not in this file stops by 20:15** (pre-run fleets, fillers, old lanes), so the rehearsal and B0 see TN10 without them. The 3 Oct halt file on the older fleet stays `halt`. **Not sure / open for debate:** on 9 Oct most of the ~1,600 tx/s outside load on keel was likely the desk's own senders.
- Read locus: synced, UTXO index, mempool, normal fee, RSS, free RAM, desk disk. Send only if synced and the UTXO index is on.
- Desk NTP: `w32tm` against time.windows.com, 5 samples. Repeat at 05:00. A move over 50 ms flags Build's confirmation times.
- Write `steps-utc.json` from the table in §5, same UTC times as the bot. That file is the step clock.
- Start the loggers in §9 now. They run to 05:00.

## 5. Schedule and rates

T0 is **21:00**. End is **Saturday 10 Oct 2026, 05:00**. His counter (Kaspa Pulse) is 21:25–05:35; it does not move T0.

**Rehearsal, 20:30–21:00**, only if keel lag ≤ 60 s at 20:15 and at 20:30 (lag = UTC now − timestamp of keel's sink block). Otherwise write **not run** with the lag and its UTC. Details: [REHEARSAL-2026-10-09.md](REHEARSAL-2026-10-09.md). Your part:

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

No light lane on Build tonight. The light tx (P2SH `OP_TRUE`, 637 mass) is the bot's optional lane, labelled **anyone-can-spend hops, not realistic payments**.

## 9. What to log

**Every second, per sender:** sender id, target, submitted, accepted, endpoint `locus`, locus mempool, submit latency. On a sample and every reject: submit and accept time, UTC with ms and `Z`. Per-transaction logging stays on.
**Every minute, per sender:** minute, sender id, node `locus`, tx_sent, five ids spread across the minute (local only). One combined Build line.
**Every 5 minutes, duplicate share, if you can read it on locus:** 60 s of locus `block-added` full blocks against locus's `getVirtualChainFromBlock` `acceptedTransactionIds`: blocks/s, tx slots/s, unique ids/s, duplicate share = 1 − unique/slots, unique accepted/s, and the same share for Build's own ids. If you cannot, write **not measured** once with the reason.
**Every 10 minutes, the Build row:** UTC, session, sender count, desk disk, `w32tm` (latest), locus synced, UTXO index, mempool, normal fee, RSS, free RAM, desk CPU, submitted tx/s, accepted tx/s, rejects by reason, miner count, mining share on locus (blocks total, ours, %), the six public pools by name, indexer health (`https://api-tn10.kaspa.org/info/health`), keel lag read on the desk, usage (or **not measured**).
**Per step:** saturation on locus (accepted under 95% of submit-OK for 60 consecutive seconds, from 60 s after start): yes or no, onset. Mean submit against target, zero seconds. Plateau label: sender-limited, node-bound, network-bound, unclear.

A required line with no reading is **not measured**, with the UTC it was due.

## 10. End and results

- 04:45 senders 0. 05:00 miner off, loggers stop, desk NTP read again.
- Results go to this repo, folder `tn10-storm-2026-10-09/build/`: README with the step table, precheck findings, gate events, fee tiers, mining share, and the CSV/JSONL data. Counts only. No txid, key, seed, host, IP or port. If you cannot push, leave the folder on the desk and write that in your last message; stp commits it.
- Commit as `STP-KAS <227352643+STP-KAS@users.noreply.github.com>`, push to main. No tags, no releases. The bot writes `COMBINED.md` from both folders. Do not ping Kaspa Pulse.
- Labels on every finding: **Claim (measured on TN10)**, **Not sure / open for debate**, **Needs more testing**.

## 11. Settled before launch (your audit, 9 Oct)

- **Claim (measured on TN10):** the gap between tx slots and accepted is duplicates across parallel blocks (48–49% of slots at 12:29 and 12:55), not off-chain loss. Transactions only in red blocks were accepted. Report `94929a9`.
- Keep 200/300 unless the quote is above 200.
- No filler aimed at 3,100 tx/s. The steps find where acceptance flattens.
- The one-side control (rows 2–4) runs before the ramp.
- The light tx is labelled anyone-can-spend.
- Cutting miners is not tonight's change. Tonight's change is one miner per side, on its own node. **Not sure / open for debate** whether it lowers the duplicate share; **Needs more testing**.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
