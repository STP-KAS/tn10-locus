> **Experimental. We are just trying this.**
>
> [Disclaimer](DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Two nodes

Private note. Kaspa Testnet-10 only. Every clock on this page is UTC.

**Goal.** The highest included tx/s the two sides can hold at the same time. Submitted and accepted stay two numbers. The score is accepted.

**Who sends where.**

| Who | Wallet | Node | When |
|---|---|---|---|
| TN10 ops, on the box | Bot only | n0, the box kaspad | Only while n0 is synced and its tip lag is at or under 300 seconds |
| Grok Build, on the desk | Build only | locus, the desk kaspad | While locus is synced and its UTXO index is on |

The bot does not send to locus. Build does not send to n0. While n0 is still syncing, the bot's senders stay off and Build keeps sending on locus. That minute's combined rate is Build's rate alone.

This page does not give the storm GO, does not lock the questions plan, and does not start a sender.

## Where this comes from

| Record | What it still is |
|---|---|
| [STP-KAS/tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions) | The questions, the Friday clock, the fee pair, and the raw files from earlier runs. |
| [STP-KAS/grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) | The private combo hub and the 8 Oct checkout sheet. |

An earlier commit of this repo sent both sides to locus and retired n0. That routing is withdrawn. The clock, the fee pair, and "never eight box runners" stay.

If this repo and `plan/NEXT-STORM-PLAN.md` disagree about a clock, a fee, or one of Kaspa Pulse's questions, the questions plan wins. If they disagree about which node a side uses, this repo wins.

## The two nodes

**n0** is the box kaspad. The bot's senders use it. The questions plan's §6a and §9 still describe that machine, including the disk guard.

**locus** is the name in the logs for the desk kaspad. Network `testnet-10`, UTXO index on. It is not a public DNS name. Build reaches it on loopback Borsh. Desk miners stay on the desk gRPC. This page does not retarget them.

Never `bore.pub`. Never `159.223.110.159`.

## Pastes and the sheet

| Who | Paste | Where it sends |
|---|---|---|
| Grok Build | [plan/PROMPT-BUILD.md](plan/PROMPT-BUILD.md) | locus |
| TN10 ops | [plan/PROMPT-BOT.md](plan/PROMPT-BOT.md) | n0, once synced |

The plan is [plan/PLAN.md](plan/PLAN.md). The monitoring tasks are [plan/MONITOR.md](plan/MONITOR.md). If a paste and the plan disagree, the plan wins.

## Clock

T0 is Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC, for 8 hours, ending Tuesday 14 Oct 2026, 05:30 UTC. The first load step is 21:40 UTC. The paced table ends at T0+175, 00:25 UTC the next day. The hours after that table have no named phase until stp chooses in the storm GO.

Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)) counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. It does not move T0.

A storm still waits for a storm GO from stp and for `steps-utc.json`. Pasting a prompt does not start it.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
