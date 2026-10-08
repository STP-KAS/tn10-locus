> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Monitor

Fields Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) asked for, pointed at **locus**. The questions plan's §3c, §4, §6, and §7 still name the measurements. Where those sections say n0, read locus. If this page and [PLAN.md](PLAN.md) disagree, the plan wins.

A number that was not read is **not measured**. No key, no seed, no address, and no txid in git.

The 8 Oct checkout rows stay in [grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo). They are not copied here. This sheet is the one that starts with locus.

## Every 10 minutes, both sides

| Field | TN10 ops, on the box | Grok Build, on the desk |
|---|---|---|
| UTC | the row time | the row time |
| Session | up or down | up or down |
| Sender count | lane runners on locus | Build senders on locus |
| Disk free | box GB, the operator machine, not the node disk | desk GB, the locus disk |
| Clock | NTP offset, two public servers | `w32tm` offset, 5 samples |
| Usage | product counter, or not measured | product counter, or not measured |
| locus | the published Borsh URL answered, synced, UTXO index on, mempool, normal fee | same node, read on loopback: synced, UTXO index, mempool, normal fee, process RSS |
| Pools | locus mempool | locus mempool, plus the six public names, each named |
| Indexer | api-tn10 `/info/health`: HTTP, `isSynced`, `acceptedTxBlockTimeDiff`, `blueScoreDiff` | same check if the box row is missing |
| Rates | submitted tx/s and accepted tx/s, two columns | submitted tx/s and accepted tx/s, two columns |
| Miners | box count, on or off, gRPC target is locus | desk count, on or off, no switch |

There is no n0 column. Lag of n0, sync of n0, and an n0 match are not rows.

## Every UTC second, per sender

Submitted and accepted stay two fields. Also: sender id, target, the endpoint, locus mempool, each named public pool, submit latency.

On a sample of transactions, and on every reject: submit time and accept time, UTC, with milliseconds and Z. Accept time is the time locus reports the transaction in the virtual chain.

Saturation, from the questions plan: accepted under 95% of submitted, sustained 60 seconds. Score it from 60 seconds after the step start. Report yes or no, and the onset UTC if yes. The other 95% is the gate in the questions plan: mean achieved send rate at least 95% of the target, with no zero seconds. The two rules stay separate.

## Every UTC minute, per sender

On top of the second log. This is the 8 Oct ask. It does not replace the second log.

| Field | What it is |
|---|---|
| minute | `YYYY-MM-DDTHH:MM:00Z` |
| sender id | that sender |
| node | `locus` |
| tx_sent | submissions by that sender in that minute |
| tx ids | five, spread across the minute, not the first five |

The node cell is the word locus. It is not "public", and it is not n0. Mempool in the same minute is locus, plus each public name when that pool was read. His accepted count is his. Do not invent it. The five ids stay in the local log. They do not go in git.

## Locus, every second, from the desk

The questions plan logged these on n0 so a flat accept rate could be labelled. The same list, on locus:

- locus process CPU and RSS
- desk total CPU and free RAM
- each sender process CPU on the machine where it runs
- locus mempool size
- locus reject reasons
- fee estimate every 10 seconds

Box CPU is the sender machine. It is not the node. A runner at one core can be sender-limited while locus is fine. Write that as sender-limited. Do not call it locus-bound.

### Plateau label

Over the step's last 10 minutes, or from saturation onset if that is earlier. One label.

**Sender-limited** if submit-OK stays under 95% of target, or any sender process stays at or above 95% of one core for 60 seconds.

**Locus-bound** if the senders are not the limit, and any of these holds for 60 seconds:

- locus unsynced
- desk free RAM under 1 GB
- locus process dead
- locus mempool at the cap the T0 flag read says, and mempool-full rejects are above 1% of submits

**Network-bound** if none of the above holds, and blocks stay at or above 90% of compute mass, or accepted tx/s stays flat within 5% from one step to the next while submit-OK rises.

**Unclear** otherwise.

The old box-bound tests that used n0's 100,000 cap, n0 RSS, and "n0 shares the box with the runners" do not transfer. n0's cap was `--ram-scale=0.1`. Locus does not run that flag. The 99,000 line is not a locus rule.

**Not sure / open for debate.** These thresholds are our choice. Network-bound means TN10 that night, with our miners on, as the questions plan already says.

## Mining share

For blocks locus sees, compare the coinbase payout with our mining addresses. Log it per second. Publish it per step: blocks total, blocks ours, share in percent. Include the miners-off step, where the share should be about 0%. The questions plan's §7 is the rule. The node the blocks are read from is locus.

## Indexer

Unchanged from the questions plan's §6, except the mempool beside it is locus:

- `GET /info/health` every 30 seconds, cache bypassed
- one already-accepted transaction polled once a minute until it is visible, give up after 30 minutes
- freeze: 3 consecutive samples (90 seconds) with 503 or timeout, or a lag above 120 seconds and rising, or a visibility delay above 300 seconds

## Clocks

NTP offset on the box and on the desk, at the start and at the end. If the desk offset moves by more than 50 ms between those two reads, flag confirmation times. The questions plan's rule is the same flag.

## Pass, for a run that claims the gate

- Mean submitted rate on each side is at least 95% of that side's target.
- No zero second on a sender that was armed for the step.
- Each second has sender id, target, submitted, accepted, endpoint, locus mempool, submit latency.
- Each minute has minute, sender id, node `locus`, tx_sent, and five local tx ids.
- Accept time is present on the sample and on every reject.
- NTP exists at the start and at the end on both sides.
- Locus match is matched/total. A missing match fails the run.
- The halt file on the old fleet still says halt.
- Git has no key, seed, address, or txid.

## Who does not watch from inside the setup

Kaspa Pulse. His count is the chain. Comparison comes to us first. This page does not send him the sheet.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
