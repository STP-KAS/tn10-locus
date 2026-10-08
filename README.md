> **Experimental. We are just trying this.**
>
> [Disclaimer](DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Locus

Private note. Kaspa Testnet-10 only. Every clock on this page is UTC.

From 8 Oct 2026, **n0 is retired**. The node both sides use is **locus**, the kaspad on the desk. This repo is that change. It does not give the storm GO, does not lock a plan, and does not start a sender.

## Where this comes from

| Record | What it still is |
|---|---|
| [STP-KAS/tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions) | The questions, the Friday clock, the fee pair, the sender counts, and the raw files from earlier runs. Public. |
| [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) | The private combo hub and the 8 Oct checkout sheet. Left as it was. |

Those two stay the record of what they already say, including every line that names n0. This repo does not rewrite them.

If this repo and `plan/NEXT-STORM-PLAN.md` in the questions repo disagree about a clock, a fee, a sender count, or one of Kaspa Pulse's questions, the questions plan wins. If they disagree about **which node**, this repo wins: the node is locus.

## The node

**locus** is the name in the logs. It is the desk kaspad, network `testnet-10`, with a UTXO index. It is not a public DNS name.

| Who | How it reaches locus |
|---|---|
| Grok Build, on the desk | Borsh wRPC on the desk loopback. The desk miners stay on the desk gRPC. This page does not retarget them. |
| TN10 ops, on the box | The Borsh URL the desk publishes for locus, and the gRPC host and port the desk publishes for box miners. |

`127.0.0.1` on the box is the box, not locus. The published host and port are not written here. A free forward changes them, and this repo does not store that hostname.

Never n0. Never `bore.pub`. Never `159.223.110.159`.

## Two pastes

| Who | Paste | Wallet | Where it sends |
|---|---|---|---|
| Grok Build, on the desk | [plan/PROMPT-BUILD.md](plan/PROMPT-BUILD.md) | Build only | locus |
| TN10 ops, on the box | [plan/PROMPT-BOT.md](plan/PROMPT-BOT.md) | Bot only | locus |

Each side spends its own wallet. The plan is [plan/PLAN.md](plan/PLAN.md). The sheet is [plan/MONITOR.md](plan/MONITOR.md). If a paste and the plan in this repo disagree, the plan wins.

## Clock

Unchanged from the questions plan. T0 is Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC, for 8 hours, ending Tuesday 14 Oct 2026, 05:30 UTC. The first load step is 21:40 UTC. The paced table ends at T0+175, 00:25 UTC the next day. The hours after that table have no named phase until stp chooses in the storm GO.

Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. It does not move T0.

A storm still waits for a storm GO from stp and for `steps-utc.json`. Pasting a prompt does not start it.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
