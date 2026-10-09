> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Monitoring tasks

The goal is the combined included rate. Each task names who does it. A number that was not read is **not measured**. No key, no seed, and no txid in git. The mining address is named in the plan.

If this page and [PLAN.md](PLAN.md) disagree, the plan wins. The 8 Oct checkout rows stay in the combo repo. They are not copied here.

The next run covers every line below. The 8 Oct n0 lines are closed, because n0 will not run. The checklist is [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). A required line with no reading is **not measured** and fails Task 10. That page does not add a demand.

## While keel syncs

Owner: the desk.

- Watch keel's block download. Leave both kaspad processes running.
- Leave the tunnel closed until keel is synced.
- When it is synced, open the tunnel and write `nodeB_wrpc` and `nodeB_grpc` in the handoff. Say both addresses. That sentence is not the storm GO.
- Until those fields are real, the bot's row says `waiting`, keel adds 0, and the combined rate is locus alone. That minute is not a failed match.

## Task 1. keel, before the bot's runner sends

Owner: the bot.

- n0 will not run. Do not read it. Read keel through the tunnel: synced, tip lag in seconds, mempool, and free disk on the box.
- The runner runs only during the storm. Send only if keel is synced, the handoff lists the tunnel, keel's lag is at or under 60 seconds (the keel health gate in the plan: over 120 seconds halve, over 300 seconds stop), and the box disk gate in the plan passes.
- If not, sender count is 0. The row says `waiting`. keel's accepted rate for that minute is 0, and it stays in the sum.

Repeat this check every 10 minutes, and at once if submits start failing because the node fell behind. Keel lag over 120 seconds mid-step halves the bot's rate. Over 300 seconds stops the bot's senders. Neither stops Build. Log keel's DAA score every 10 seconds and the public node's every 60 seconds. A freeze is keel's DAA score not moving for 60 seconds or more while the public node moves. Write each freeze with its start and length. On 9 Oct keel froze for 3–5 minutes about every 10 minutes from about 14:05 UTC.

## Task 2. Locus, before Build sends

Owner: Grok Build.

- Read synced, UTXO index, mempool, normal fee, process RSS, free RAM, and free disk.
- Send only if synced and the UTXO index is on, on loopback Borsh.
- If free RAM is under 1 GB, or the process dies, stop Build's senders. Keep them on locus.
- Before T0, find what runs on the desk about every 10 minutes: sender steps or restarts, locus or keel pruning, Defender, Task Scheduler. Write each with its times. Desk CPU, RAM and disk for both kaspad processes go on every 10-minute row.

## Task 3. The 10-minute row

Owner: the desk writes the sheet. The box prints its block. A missing block stays **not measured**. Do not invent the other side.

| Field | Bot, keel | Build, locus |
|---|---|---|
| UTC | row time | row time |
| Session | up, down, or waiting | up or down |
| Sender count | lane runners, or 0 while waiting | Build senders |
| Disk free | box GB | desk GB |
| Clock | NTP offset, two public servers | `w32tm`, 5 samples |
| Node | synced, lag seconds, mempool, CPU | synced, UTXO index, mempool, normal fee, RSS, free RAM |
| Rates | submitted tx/s and accepted tx/s | submitted tx/s and accepted tx/s |
| Combined | sum of the two submitted rates, and sum of the two accepted rates | same two sums, one line for the minute |
| Pools | keel mempool | locus mempool, plus the six public names, each named |
| Indexer | api-tn10 `/info/health` | same check if the box row is missing |
| Miners | 1 bot miner on keel, through the keel tunnel, or off while keel is unsynced | 1 Build miner on locus. No desk miner on keel |

Rows are due on the questions plan's clock once a run is armed. Between runs, a row is still owed if a side is sending.

## Task 4. Every UTC second, per sender

Owner: the side that sends.

One line: sender id, target, submitted, accepted, endpoint (`keel` or `locus`), that node's mempool, submit latency.

On a sample of transactions, and on every reject: submit time and accept time, UTC, with milliseconds and Z.

Saturation, per side: accepted under 95% of submitted, sustained 60 seconds, scored from 60 seconds after that side's start. Report yes or no, and the onset if yes. The other 95% is mean send rate against that side's target, with no zero seconds, and only for seconds the side was armed. A waiting bot is not a zero-second failure.

## Task 5. Every UTC minute, per sender

On top of the second log. This is the 8 Oct ask.

| Field | What it is |
|---|---|
| minute | `YYYY-MM-DDTHH:MM:00Z` |
| sender id | that sender |
| node | `keel` for the bot's runner, `locus` for Build |
| tx_sent | submissions by that sender in that minute |
| tx ids | five, spread across the minute, not the first five |

Add one combined line for the same minute: both submitted sums, both accepted sums. His accepted count is his. Do not invent it. The five ids stay in the local log.

## Task 6. Label a flat accept rate

Owner: the desk, from both logs. One label per side, over the step's last 10 minutes, or from saturation onset.

**Sender-limited** if that side's submit-OK stays under 95% of its target, or any of its sender processes stays at or above 95% of one core for 60 seconds.

**Node-bound** if the senders are not the limit and, for 60 seconds, that side's node is unsynced, its mempool is at the cap read from its own flags, or (locus only) desk free RAM is under 1 GB or the process is dead.

n0's cap in the questions plan is about 100,000 transactions, from `--ram-scale=0.1`. Locus does not run that flag. Do not apply 99,000 to locus.

**Network-bound** if neither side is sender-limited or node-bound, and blocks stay at or above 90% of compute mass, or the combined accepted rate stays flat within 5% while combined submit-OK rises.

**Unclear** otherwise.

**Not sure / open for debate.** The thresholds are our choice. Network-bound means TN10 that night, with our miners on.

## Task 7. Indexer

Owner: whichever side is up. The box if both are up.

- `GET https://api-tn10.kaspa.org/info/health` every 30 seconds, cache bypassed. Log HTTP, `isSynced`, `acceptedTxBlockTimeDiff`, `blueScoreDiff`.
- Freeze: 3 consecutive samples (90 seconds) with 503 or timeout, or a lag above 120 seconds and rising, or a visibility delay above 300 seconds.
- One already-accepted id polled once a minute until it is visible, give up after 30 minutes. The id stays local.

## Task 8. Mining share

Owner: each node, for the blocks it sees.

Per second, then published per step: blocks total, blocks ours, share in percent. The miners-off step should read about 0%. The bot runs exactly 1 miner, on keel through the tunnel, paying the Grok Bot address, user agent suffix `stp grok bot`, only while keel is synced. Build runs exactly 1 miner, on locus. No desk miner on keel. No bot miner on locus. The questions plan's §7 is the rule. Count the share on the blocks keel sees, and on the blocks locus sees.

## Task 8a. Duplicate share

Owner: the bot on keel. Build on locus, if it can read it.

Every 5 minutes, and per step: 60 seconds of full blocks from `block-added`, against the transactions the virtual chain accepted (`getVirtualChainFromBlock`, `acceptedTransactionIds`). Write tx slots per second (non-coinbase transactions summed over all blocks), unique ids per second, duplicate share = 1 − unique/slots, unique accepted per second, and our block share. A window where keel accepted under 95% of the window's unique ids is keel lag, not network data. Ids stay local. **Needs more testing:** whether the per-node split lowers the share.

## Task 9. Clocks

NTP offset on the box and on the desk, at the start and at the end of a run. If the desk offset moves by more than 50 ms between those two reads, flag Build's confirmation times.

## Task 10. Pass

A run that claims the combined goal shows all of these:

- Combined accepted tx/s is on the sheet, next to each side's own accepted tx/s.
- The bot's minutes are either `keel` with a match, or `waiting` with sender count 0. A missing keel sync check fails the bot's part. The runner is off outside the storm.
- Build's minutes say `locus`, and the match is matched over submitted on locus.
- No zero second on a sender that was armed.
- Each minute has sender id, node name, tx_sent, and five local tx ids.
- The halt file on the old fleet still says halt.
- Git has no key, no seed, and no txid. The mining address is the one in the plan.

## Who does not watch from inside the setup

Kaspa Pulse. His count is the chain. Comparison comes to us first. This page does not send him the sheet.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
