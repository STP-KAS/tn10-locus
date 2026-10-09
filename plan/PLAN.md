> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Plan

TN10 only. Every clock time in this repo is UTC. This page does not lock the questions plan.

**Start.** Sending this GitHub to Grok Build or to the bot means go: start the operation. The bot's runner and the bot's one miner use the tunnel to keel, and the runner runs only during the storm, apart from the rehearsal in §3a. n0 will not run.

**Launch files.** Tonight is launched by pasting [GO-BOT.md](GO-BOT.md) into the bot and [GO-BUILD.md](GO-BUILD.md) into Grok Build. Pasting is the GO for that side. Each is self-contained, with the exact UTC schedule and rates.

The question list, the step table, and the fee pair stay in [NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md). This page sets the node split, the mining split, and the combined goal. Under the repo's own rule, a node or miner question is decided here. What was measured is [monitoring-result/](../monitoring-result/README.md). This page stays the plan.

## 1. Goal

Reach the highest included tx/s the two sides can hold together.

- Each side pushes its own node as hard as that node still accepts.
- The score for a minute is the sum of the two accepted rates. Submitted is the other number.
- Block mass still tops out near 305 transactions in a block, about 3,024 included tx/s for a transaction near 1,624 grams, at 10 blocks per second. That is the questions plan's mass note. Two nodes do not double it. They share one chain.
- A submit spike with orphans is not the score. A fat mempool on a synced node, with the chain already full, is the cap until the logs say otherwise.
- While keel is unsynced, or fails the keel health gate in §3, the bot's runner contributes 0 and Build's accepted rate is the whole score.

## 2. Who sends where

A process that signs and sends is a sender. The whole setup is a runner. TN10 ops is the operator.

| Side | Wallet | Node | Senders | Miners |
|---|---|---|---|---|
| The bot's runner | Bot only | keel only | Up to 15 runners, 4 connections each, only during the storm, behind the keel health gate (§3) | Exactly 1, on keel only |
| Grok Build | Build only | locus only | 4 fixed senders on a paced step. On a max step, more only while locus stays up | Exactly 1, on locus only |

Rules:

- The bot's runner uses keel, the second kaspad on the desk, through the tunnel stp provides. It does not use `ws://127.0.0.1:17310` from the box. That socket is keel's own Borsh port on the desk. Until the handoff lists the tunnel, the runner waits. It runs only during the storm and the rehearsal (§3a). It sends only while keel is synced and passes the keel health gate in §3. Otherwise those senders stay off. n0 will not run.
- Build sends on locus for every paced step, the long hold, and the max step. Loopback Borsh on the first desk kaspad.
- The bot's runner cap on keel is 15. stp raised it from 6 to 15 in chat on 9 Oct 2026 (11:15–11:23 UTC), and 15 ran on keel that day at under 10% CPU each. This is a deviation from the questions plan's count, written with that time and reason. "Never eight" stays for any box runner that is not on keel. Eight collapsed in the 1–3 Oct storm.
- No auto-scale. No mempool pause inside a step. Each sender spends its own coins.
- Depth 2, in-flight 48, four connections, on a paced step.
- The bot runs exactly 1 miner: box CPU `kaspa-miner`, 1 thread, on keel only, through the same tunnel, gRPC host and port from the handoff. Coinbase pays the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`. User agent suffix `stp grok bot`. Mine only while keel is synced. keel's own desk gRPC is `127.0.0.1:16310`. That is not the box's address. No bot miner on locus.
- Build runs exactly 1 miner, on locus only. No desk miner on keel, before or after keel syncs.
- On 8 Oct 2026, ten sender processes on the desk faulted locus, and twelve drove free RAM to about half a gigabyte. Those were Build's own senders on one machine. The bot's runner is not added on top of them. If locus dies, or desk free RAM falls under 1 GB, Build stops.

`bore.pub` and `159.223.110.159` stay closed.

### 2a. Why one miner per node

stp's decision, 9 Oct 2026, 16:06 UTC: each side mines where it sends. The bot sends to keel and mines on keel. Build sends to locus and mines on locus.

- **Claim (measured on TN10):** the 9 Oct keel report, [monitoring-result/bot-result](../monitoring-result/bot-result/README.md), commit `94929a9`, found 48–49% of tx slots in blocks were duplicates of a transaction already in a parallel block (12:29 and 12:55 UTC). In 3 of the 4 valid windows, 97–100% of distinct transactions were accepted, including the ones seen only in red blocks.
- **Not sure / open for debate:** splitting miners and senders per node makes blocks carry more distinct transactions.
- **Needs more testing:** the one-side control in §3b measures it.

## 3. Clock and gates

This evening only. No fallback day.

T0 is Friday 9 Oct 2026, 21:00 UTC. End is Saturday 10 Oct 2026, 05:00 UTC. Eight hours.

The old line "Monday 13 Oct 2026, 21:30 UTC" is dropped. 13 Oct 2026 is a Tuesday, not a Monday. This run is not Monday 12 Oct and not Tuesday 13 Oct.

B0 is the first 10 minutes. First load step is 21:10 UTC: the one-side control in §3b, then the questions plan's 2× step at 21:40 UTC. Paced table still ends 00:25 UTC (T0+205: the questions plan's 175 minutes plus the 30-minute control). The storm GO names the hours after 00:25 UTC: the GO files run a long hold 00:25–04:45 UTC at each side's last clean rate, then a final drain to 05:00 UTC.

His counter stays 21:25 UTC through 05:35 UTC. It does not move T0. Our T0 is 25 minutes before that counter. Both clocks are written so the gap is visible.

Before any send, all three:

1. This GitHub has been sent to Grok Build or to the bot. That is the storm GO. A dry-run GO is not this.
2. `steps-utc.json`, with a UTC start and a UTC end for every step. Each side writes it from the table in its GO file.
3. The clock is at or after the first time in that file. The runner runs only during the storm.

B0 is the first 10 minutes. Lane senders stay off. Build sends nothing in B0.

### 3a. Rehearsal

A 30-minute rehearsal runs before T0 at a fixed time, 20:30–21:00 UTC, only if keel's lag is at or under 60 seconds at 20:15 UTC (T0 − 45) and at 20:30 UTC. Otherwise it is skipped and written **not run**. Steps and pass rules: [REHEARSAL-2026-10-09.md](REHEARSAL-2026-10-09.md). stp approved it on 9 Oct 2026, 16:08 UTC. It does not move T0 and it is not the storm GO.

### 3b. One-side control, before the ramp

Three steps at fixed rates, right after B0, before the 2× step. Both single miners stay on through all three.

| Step | UTC | Bot on keel | Build on locus |
|---|---|---|---|
| C1, bot alone | 21:10–21:20 | 60 tx/s | 0 |
| C2, Build alone | 21:20–21:30 | 0 | 60 tx/s |
| C3, both | 21:30–21:40 | 60 tx/s | 60 tx/s |

Per step: tx slots per second in blocks, unique ids per second, duplicate share = 1 − unique/slots, and unique accepted tx/s from keel's `getVirtualChainFromBlock` `acceptedTransactionIds`. Locus gives the same reading if Build can read it. Each step is at least 10 minutes. If keel fails its gate in C1 or C3, the bot's cell is `waiting` and that step is written as Build-only data, not as a control.

The questions plan's table follows from 21:40 UTC, unchanged in step lengths, with every row 30 minutes later. `steps-utc.json` writes the shifted times. This is a deviation from that table, written with a time and a reason: stp's decision of 9 Oct 2026, 16:06 UTC. **Needs more testing.**

The questions plan's miners-off control (its §3b) still runs. "All our miners off" now means the bot's one miner and Build's one miner.

### Bot rate, keel

- Start at 60 tx/s on keel. **Claim (measured on TN10):** 60 tx/s was the clean level on 9 Oct (100% eventual, p90 ≤ 7 s). 100 and 120 broke under 20,000–40,000 transactions of outside mempool.
- Step up only at a step boundary, and only while the last step held: eventual accept ≥ 99%, p90 submit-to-accept ≤ 10 s, keel lag ≤ 60 s. Otherwise hold the last clean level.
- Nothing changes inside a step except the keel health gate.
- Max 15 runners.
- The bot's part of a paced step is the lower of its share in the questions plan and its gated level. The gap is written on the row. Build does not change its own target mid-step to cover it.

### Bot gate, keel

From the questions plan's §9, for the box only:

- Go only with at least 35 GB free on the box at T0. From 28 GB through 35 GB, the bot's steps shrink to 10 minutes and that is written as a deviation. Below 28 GB, the bot does not send. Build is not stopped by the box disk.
- n0 will not run, so the box does not keep disk aside for n0 pruning. A guard stop on the box ends the bot's senders. It does not by itself stop Build.
- **Keel health gate.** No bot sending unless keel's lag is at or under 60 seconds. Over 120 seconds, the bot halves its rate. Over 300 seconds, the bot's senders stop. They resume, at the halved rate, once lag is back at or under 60 seconds. The bot's miner stops over 300 seconds too.
- **Claim (measured on TN10):** on 9 Oct, from about 14:05 UTC, keel froze for 3–5 minutes about every 10 minutes, with no bot load and nobody at the desk, while the public node ran about 9.6 DAA per second. **Not sure / open for debate:** something on the desk runs on a 10-minute schedule.
- keel unsynced, the tunnel not in hand, or failing the health gate, means the bot's runner waits. Unsynced also stops the bot's miner. The row says waiting. keel still counts as 0 in that minute's sum. It is not a failed match. The runner stays off outside the storm.

### Build gate, locus

- locus synced, UTXO index on, read on the loopback.
- Desk free RAM stays at or above 1 GB. Under that, Build stops.
- The box disk figure is not this gate.
- **Pre-check, before T0.** Find what runs on the desk about every 10 minutes: Build's sender steps or restarts, locus or keel pruning, Defender scans of the kaspad data folders, and Task Scheduler. Write each one found with its times. Nothing found is written as nothing found.

### Still open

- The storm GO is this GitHub sent to Grok Build or to the bot. It is open until that send.
- `steps-utc.json`.
- The questions plan is still unlocked. At T0 the run log writes the SHA of the last commit that changed `plan/NEXT-STORM-PLAN.md`, and the SHA of this file.
- The hours after 00:25 UTC are named in the GO files.

## 4. Fees

The pair stays **200 and 300** sompi/gram, cap **600**, until a multi-hour seen-accepted rate over **2,207** is written into the questions plan.

Each side reads the quote from its own node at the step start and freezes it. Half the lanes at 1x, half at 1.5x. If that node's normal quote is already above 200, that side does not start. The other side still may.

**Claim (measured on TN10):** on 9 Oct, 1.5× (300) beat 1× (200) by about 0.5 s at p50, and paying the live quote changed little. A higher fee reorders transactions inside full blocks. It does not add capacity.

### Light lane, the bot, optional

Only if keel passes its health gate, in small amounts. P2SH with redeem script `OP_TRUE`, 1 input, 1 output, unsigned, 637 mass. **Claim (measured on TN10):** standard-valid on keel, 9 Oct 13:47 UTC probe (a 1,701-mass fund and three 637-mass hops in keel's mempool). On-chain inclusion is checked in the rehearsal. Every number from it is labelled **anyone-can-spend hops, not realistic payments**. It runs only if the rehearsal's light-lane step passed.

## 5. Acceptance

The bot's accept time is the time keel reports the transaction in its mempool. Build's accept time is the time locus reports it. A submit acknowledgement is the other counter on each side. Kaspa Pulse's count is what landed in blocks. Those are not the same number.

Kaspa Pulse counts the chain. His count and our combined accepted count stay two numbers until the same ids are on both clocks. Comparison comes to this side first. This page does not ping him.

The bot's match is on keel: matched over submitted. Build's match is on locus. A side that was waiting does not owe a match for that minute.

## 6. Monitoring

The sheet is [MONITOR.md](MONITOR.md). The checklist for this run is [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). One owner each. A missing required line is **not measured** and fails the pass.

**While keel syncs.** The desk watches the block download. Both kaspad processes stay up. The tunnel stays closed until keel is synced. When it is synced, the desk opens the tunnel, writes `nodeB_wrpc` and `nodeB_grpc` in the handoff, and says both addresses. That sentence is not the storm GO. Until those fields are real, the row says `waiting`, keel adds 0, and the combined rate is locus alone.

**From T0.** The sheet runs through B0, with the two single miners on and both runners off, then through the one-side control, then through every load step. Duplicate share per step, keel lag, and DAA per second from keel and from the public node are on every row. The desk writes the combined row. The box prints its own block. A waiting keel minute is not a failed match and does not stop Build.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
