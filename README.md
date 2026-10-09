> **Experimental. We are just trying this.**
>
> [Disclaimer](DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Two nodes

Private note. Kaspa Testnet-10 only. Every clock on this page is UTC.

**Goal.** The highest included tx/s the two sides can hold at the same time. Submitted and accepted stay two numbers. The score is accepted. How a block gets past 3,000 included payments, and why a second runner does not double it, is [goal/README.md](goal/README.md). That page does not start the storm and does not move T0.

**Start.** Sending this GitHub to Grok Build or to the bot means go: start the operation. The same sentence is the forward rule in [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) `TWO-NODES.md`.

**Who sends where.**

| Who | Wallet | Node | When |
|---|---|---|---|
| The bot's runner | Bot only | keel, the second kaspad on the desk | Only during the storm, and only while keel is synced and its tip lag is at or under 300 seconds |
| Grok Build, on the desk | Build only | locus, the first desk kaspad | While locus is synced and its UTXO index is on |

Outside the storm the bot's runner stays off. While keel is still syncing, that runner stays off and Build keeps sending on locus. That minute's combined rate is Build's rate alone.

This page does not lock the questions plan.

## Where this comes from

| Record | What it still is |
|---|---|
| [STP-KAS/tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions) | The questions, the Friday clock, the fee pair, and the raw files from earlier runs. |
| [plan/NEXT-RUN-MONITOR.md](plan/NEXT-RUN-MONITOR.md) | The next run's monitor. Every line already in the plan. A blank required line fails the pass. |
| [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) | The private combo hub and the 8 Oct checkout sheet. |

An earlier commit of this repo sent both sides to locus. That routing stays withdrawn. Build stays on locus. The bot uses keel. n0 will not run. The clock, the fee pair, and "never eight box runners" stay.

If this repo and `plan/NEXT-STORM-PLAN.md` disagree about a clock, a fee, or one of Kaspa Pulse's questions, the questions plan wins. If they disagree about which node a side uses, this repo wins.

## The two nodes

**locus** is the first kaspad on this desk. Network `testnet-10`, UTXO index on. It is not a public DNS name. Build reaches it on loopback Borsh. The node cell is `locus`.

**keel** is the second kaspad on this desk. Same network, UTXO index on. It is not a public DNS name. The handoff still writes `node=desk-nodeB`. New logs use `keel`. On the desk its own sockets are Borsh `ws://127.0.0.1:17310` and gRPC `127.0.0.1:16310`. The bot does not use those loopback addresses. The bot's runner and the bot's miners use the tunnel stp provides. The runner uses the tunnel's Borsh `ws://` address, only during the storm, and only while keel is synced and tip lag is at or under 300 seconds. The miners use the tunnel's gRPC host and port, pay the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`, and mine only while keel is synced. Until the handoff lists the tunnel, both wait. Do not invent a host.

**keel is already in the score.** Read at 2026-10-09T07:59:26Z: block download 69%, last block 2026-10-08T17:03:33Z, not synced, tunnels closed. Those minutes contribute 0 from keel and the row says `waiting`. The combined rate is locus alone. Desk miners stay on locus until keel is synced.

**n0 will not run.** It is the box kaspad. Do not start it, resync it, or keep disk aside for its pruning. The questions plan's older §6a and §9 sentences about n0 are the record of that machine. They are not this operation.

`bore.pub` and `159.223.110.159` stay closed.

## Pastes and the sheet

| Who | Paste | Where it sends |
|---|---|---|
| Grok Build | [plan/PROMPT-BUILD.md](plan/PROMPT-BUILD.md) | locus |
| The bot's runner | [plan/PROMPT-BOT.md](plan/PROMPT-BOT.md) | keel, only during the storm |

The plan is [plan/PLAN.md](plan/PLAN.md). The monitoring tasks are [plan/MONITOR.md](plan/MONITOR.md). If a paste and the plan disagree, the plan wins.

## Clock

T0 is Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC, for 8 hours, ending Tuesday 14 Oct 2026, 05:30 UTC. The first load step is 21:40 UTC. The paced table ends at T0+175, 00:25 UTC the next day. The hours after that table have no named phase until stp chooses in the storm GO.

Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. It does not move T0.

Sending this GitHub to Grok Build or to the bot is the storm GO. The runner still runs only during the storm, and it still needs `steps-utc.json` for the step times. The hours after 00:25 UTC stay unnamed until that GO chooses them.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
