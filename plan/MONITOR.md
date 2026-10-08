> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Monitoring tasks

The goal is the combined included rate. Each task names who does it. A number that was not read is **not measured**. No key, no seed, no address, and no txid in git.

If this page and [PLAN.md](PLAN.md) disagree, the plan wins. The 8 Oct checkout rows stay in the combo repo. They are not copied here.

The next run covers every line below, including the lines 8 Oct left unread. The checklist is [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). A required line with no reading is **not measured** and fails Task 10. That page does not add a demand.

## Task 1. n0, before the bot sends

Owner: TN10 ops.

- Read synced, tip lag in seconds, mempool, and free disk.
- Send only if synced and lag is at or under 300 seconds, and the box disk gate in the plan passes.
- If not, sender count is 0. The row says `waiting`. Do not point the runners at locus.

Repeat this check every 10 minutes, and at once if submits start failing because the node fell behind. Falling behind mid-step stops the bot's senders. It does not stop Build.

## Task 2. Locus, before Build sends

Owner: Grok Build.

- Read synced, UTXO index, mempool, normal fee, process RSS, free RAM, and free disk.
- Send only if synced and the UTXO index is on, on loopback Borsh.
- If free RAM is under 1 GB, or the process dies, stop Build's senders. Do not move them to n0.

## Task 3. The 10-minute row

Owner: the desk writes the sheet. The box prints its block. A missing block stays **not measured**. Do not invent the other side.

| Field | Bot, n0 | Build, locus |
|---|---|---|
| UTC | row time | row time |
| Session | up, down, or waiting | up or down |
| Sender count | lane runners, or 0 while waiting | Build senders |
| Disk free | box GB | desk GB |
| Clock | NTP offset, two public servers | `w32tm`, 5 samples |
| Node | synced, lag seconds, mempool, CPU | synced, UTXO index, mempool, normal fee, RSS, free RAM |
| Rates | submitted tx/s and accepted tx/s | submitted tx/s and accepted tx/s |
| Combined | sum of the two submitted rates, and sum of the two accepted rates | same two sums, one line for the minute |
| Pools | n0 mempool | locus mempool, plus the six public names, each named |
| Indexer | api-tn10 `/info/health` | same check if the box row is missing |
| Miners | box count, on or off, still on n0 | desk count, on or off, no switch |

Rows are due on the questions plan's clock once a run is armed. Between runs, a row is still owed if a side is sending.

## Task 4. Every UTC second, per sender

Owner: the side that sends.

One line: sender id, target, submitted, accepted, endpoint (`n0` or `locus`), that node's mempool, submit latency.

On a sample of transactions, and on every reject: submit time and accept time, UTC, with milliseconds and Z.

Saturation, per side: accepted under 95% of submitted, sustained 60 seconds, scored from 60 seconds after that side's start. Report yes or no, and the onset if yes. The other 95% is mean send rate against that side's target, with no zero seconds, and only for seconds the side was armed. A waiting bot is not a zero-second failure.

## Task 5. Every UTC minute, per sender

On top of the second log. This is the 8 Oct ask.

| Field | What it is |
|---|---|
| minute | `YYYY-MM-DDTHH:MM:00Z` |
| sender id | that sender |
| node | `n0` for the bot, `locus` for Build |
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

Per second, then published per step: blocks total, blocks ours, share in percent. The miners-off step should read about 0%. Box miners count on n0. Desk miners count on locus. The questions plan's §7 is the rule.

## Task 9. Clocks

NTP offset on the box and on the desk, at the start and at the end of a run. If the desk offset moves by more than 50 ms between those two reads, flag Build's confirmation times.

## Task 10. Pass

A run that claims the combined goal shows all of these:

- Combined accepted tx/s is on the sheet, next to each side's own accepted tx/s.
- The bot's minutes are either `n0` with a match, or `waiting` with sender count 0. A missing n0 sync check fails the bot's part.
- Build's minutes say `locus`, and the match is matched over submitted on locus.
- No zero second on a sender that was armed.
- Each minute has sender id, node name, tx_sent, and five local tx ids.
- The halt file on the old fleet still says halt.
- Git has no key, seed, address, or txid.

## Who does not watch from inside the setup

Kaspa Pulse. His count is the chain. Comparison comes to us first. This page does not send him the sheet.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
