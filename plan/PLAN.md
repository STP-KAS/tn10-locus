> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Plan

TN10 only. UTC only. This page does not give the storm GO, does not lock the questions plan, and does not start a sender.

The question list, the step table, and the fee pair stay in [NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md). This page sets the node split and the combined goal.

## 1. Goal

Reach the highest included tx/s the two sides can hold together.

- Each side pushes its own node as hard as that node still accepts.
- The score for a minute is the sum of the two accepted rates. Submitted is the other number.
- Block mass still tops out near 305 transactions in a block, about 3,024 included tx/s for a transaction near 1,624 grams, at 10 blocks per second. That is the questions plan's mass note. Two nodes do not double it. They share one chain.
- A submit spike with orphans is not the score. A fat mempool on a synced node, with the chain already full, is the cap until the logs say otherwise.
- While n0 is unsynced, the bot contributes 0 and Build's accepted rate is the whole score.

## 2. Who sends where

A process that signs and sends is a sender. The whole setup is a runner. TN10 ops is the operator.

| Side | Wallet | Node | Senders |
|---|---|---|---|
| TN10 ops | Bot only | n0 | 6 runners, 4 connections each, once n0 is synced |
| Grok Build | Build only | locus | 4 fixed senders on a paced step. On a max step, more only while locus stays up |

Rules:

- The bot sends only while n0 is synced and tip lag is at or under 300 seconds. Otherwise those senders stay off. Do not point them at locus to fill the gap.
- Build sends on locus for every paced step, the long hold, and the max step. Loopback Borsh. Do not send those transactions to n0 or to a public node.
- A seventh box runner only on the max step. Never eight. Eight collapsed in the 1–3 Oct storm. The questions plan is the source of that count.
- No auto-scale. No mempool pause inside a step. Each sender spends its own coins.
- Depth 2, in-flight 48, four connections, on a paced step.
- Desk miners stay on the desk gRPC. This page does not switch them. Box miners stay on n0. They do not mine against locus.
- On 8 Oct 2026, ten sender processes on the desk faulted locus, and twelve drove free RAM to about half a gigabyte. Those were Build's own senders on one machine. Box runners are not added on top of them. If locus dies, or desk free RAM falls under 1 GB, Build stops. The bot does not move onto the desk.

Never `bore.pub`. Never `159.223.110.159`.

## 3. Clock and gates

T0 is Friday 9 Oct 2026, 21:30 UTC, else Monday 13 Oct 2026, 21:30 UTC. First load step 21:40 UTC. End 05:30 UTC the next morning. Paced table ends 00:25 UTC. The hours after 00:25 have no name until the storm GO names them, or ends the storm at 00:25. This page does not choose.

Before any send, all three:

1. A storm GO from stp. A dry-run GO is not this.
2. `steps-utc.json`, with a UTC start and a UTC end for every step.
3. The clock is at or after the first time in that file.

B0 is the first 10 minutes. Lane senders stay off. Build sends nothing in B0.

### Bot gate, n0

From the questions plan's §9, for the box only:

- Go only with at least 35 GB free on the box at T0. From 28 GB through 35 GB, the bot's steps shrink to 10 minutes and that is written as a deviation. Below 28 GB, the bot does not send. Build is not stopped by the box disk.
- Keep about 19 GB free for n0 pruning. A guard stop on the box ends the bot's senders. It does not by itself stop Build.
- n0 unsynced, or more than 300 seconds behind, means the bot waits. The row says waiting. It is not a failed match.

### Build gate, locus

- locus synced, UTXO index on, read on the loopback.
- Desk free RAM stays at or above 1 GB. Under that, Build stops.
- The box disk figure is not this gate.

### Still open

- Storm GO.
- `steps-utc.json`.
- The questions plan is still unlocked. At T0 the run log writes the SHA of the last commit that changed `plan/NEXT-STORM-PLAN.md`, and the SHA of this file.
- The unnamed hours after 00:25 UTC.

## 4. Fees

The pair stays **200 and 300** sompi/gram, cap **600**, until a multi-hour seen-accepted rate over **2,207** is written into the questions plan.

Each side reads the quote from its own node at the step start and freezes it. Half the lanes at 1x, half at 1.5x. If that node's normal quote is already above 200, that side does not start. The other side still may.

## 5. Acceptance

The bot's accept time is the time n0 reports the transaction. Build's accept time is the time locus reports it. A submit acknowledgement is the other counter on each side.

Kaspa Pulse counts the chain. His count and our combined accepted count stay two numbers until the same ids are on both clocks. Comparison comes to this side first. This page does not ping him.

The bot's match is on n0: matched over submitted. Build's match is on locus. A side that was waiting does not owe a match for that minute.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
