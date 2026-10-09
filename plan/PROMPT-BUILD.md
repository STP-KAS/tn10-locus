> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for Grok Build

For tonight, paste [GO-BUILD.md](../go/build/GO-BUILD.md) instead. It is the launch file. This page is the standing prompt. Paste this into Grok Build on the desk. Sending this GitHub to Grok Build or to the bot means go: start the operation. This file does not lock the questions plan and does not spend.

Build uses **locus**, the first desk kaspad. The bot's runner uses keel, the second kaspad on the desk, and it runs only during the storm and the rehearsal. Each side mines where it sends: one Build miner on locus, one bot miner on keel. If this file and [PLAN.md](PLAN.md) disagree, the plan wins.

## Goal

The highest included tx/s the two sides can hold together. This side's score is transactions locus accepted. The combined score adds the bot's accepted rate. Do not invent the bot's number.

## Before any send

Stop unless all three are true:

- This GitHub has been sent to Grok Build or to the bot. That is the storm GO.
- `steps-utc.json` is in hand.
- The clock is at or after the first time in that file.

Also stop this side unless locus is synced and its UTXO index is on. If desk free RAM is under 1 GB, do not send.

**Pre-check.** Before T0, find what runs on the desk about every 10 minutes: this side's sender steps or restarts, locus or keel pruning, Defender scans of the kaspad data folders, Task Scheduler. Write each one with its times. On 9 Oct keel froze for 3–5 minutes about every 10 minutes from about 14:05 UTC, with no bot load and nobody at the desk.

**Rehearsal.** Before T0, join [REHEARSAL-2026-10-09.md](REHEARSAL-2026-10-09.md) if keel is healthy: 1 miner on locus, and 60 tx/s in the 3-minute Build-only and both blocks, 20:53–20:59 UTC. The rehearsal is fixed at 20:30–21:00 UTC. If keel is not healthy at 20:15 UTC, it is **not run**.

The hours after 00:25 UTC are named in [GO-BUILD.md](../go/build/GO-BUILD.md): long hold to 04:45 UTC, final drain to 05:00 UTC.

keel's sync is not this side's gate. If the bot's runner is waiting, keep this side on locus. The bot's one miner uses the keel tunnel and is not this side's process.

## This side

- TN10 only. Network `testnet-10`. The Build wallet only.
- Every step goes to locus. Loopback Borsh. Not n0. Not a public node. Not an old public tunnel relay.
- One-side control after B0: 21:10–21:20 UTC this side at 0, 21:20–21:30 UTC this side alone at 60 tx/s, 21:30–21:40 UTC both, 60 tx/s each. Then the paced steps.
- Four fixed senders on a paced step. Depth 2. In-flight 48. Four connections. No auto-scale.
- Fee frozen from locus's quote at 200 and 300 sompi/gram, cap 600, unless the questions plan has a later long window over 2,207 seen-accepted. If locus's normal quote is already above 200, do not start. A higher fee reorders. It does not add capacity.
- Leave the 3 Oct halt on the older fleet in place.
- Exactly 1 miner, on locus only. No desk miner on keel, before or after keel syncs. Log the count.
- Keys stay on the desk. Do not print a key, a seed, or a wallet file.

## Logs

Do the Build columns of [MONITOR.md](MONITOR.md), and every Build line in [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). Per-transaction logging stays on. Per minute the node cell is `locus`. Five tx ids stay local. The 10-minute row includes locus mempool, the six public pools by name, indexer health, desk disk, free RAM, desk CPU, miner count, submit tx/s, accepted tx/s, and the duplicate share from locus if it can be read. B0 is the first 10 minutes. Send nothing in B0. A blank required line fails the pass.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
