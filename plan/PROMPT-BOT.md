> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for the operator

Paste this into TN10 ops on the box. This file does not start the storm, does not lock the plan, and does not spend.

The node is **locus**, the desk kaspad. n0 is retired. If this file and [PLAN.md](PLAN.md) disagree, the plan wins. If the plan and the questions repo's `NEXT-STORM-PLAN.md` disagree on a clock, a fee, or a sender count, the questions plan wins.

## Goal

One combo with Grok Build, on one UTC clock. Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC, for 8 hours.

Kaspa Pulse counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. Do not start at 21:00 or at 21:25.

## Before any send

Stop unless all three are true:

- stp has given the storm GO. This file does not give it.
- `steps-utc.json` is in hand. Box and Build use the same UTC times.
- The clock is at or after the first time in that file.

Do not wait for n0 to sync. Do not read an n0 lag. The coins are the Bot wallet's mature UTXOs as locus returns them.

The hours from 00:25 UTC to 05:30 UTC have no named phase. If the storm GO does not name them, or does not end the storm at 00:25, stop and ask.

## This side

- TN10 only. Network `testnet-10`.
- The Bot wallet only.
- Borsh URL: the one the desk published for locus. Encoding Borsh. If `getServerInfo` is not `testnet-10`, or the node is not synced, or it has no UTXO index, stop.
- When that URL stops answering, take the next pair the desk publishes. Do not guess a host. Do not fall back to n0.
- `127.0.0.1` on this box is not locus.
- Six runners, four connections each, for the paced steps. A seventh runner only on the max step. Never eight.
- Depth 2 on a paced step. Fee frozen at 200 and 300 sompi/gram, cap 600, from the locus quote, unless the questions plan has moved that pair. If the normal quote is already above 200, do not start.
- Build's share of each paced step is 25%. This side sends the rest. The max step is uncapped for both.
- Box miners, when they run, use the gRPC host and port the desk published for locus. One thread each. Log the count.
- Do not send to n0, to `bore.pub`, or to `159.223.110.159`.
- Keys stay on the box. Do not print a key, a seed, a wallet file, or an address.

## Logs

Per second: sender id, target, submitted, accepted, endpoint, locus mempool. Times are UTC with milliseconds and Z. Accepted means locus has the transaction in the virtual chain.

Per minute, one local line per sender: minute, sender id, node `locus`, tx_sent, five tx ids spread across the minute. The ids stay local.

Locus match is this side's job: matched/total against locus. There is no n0 match.

The lane runners stay off in B0, in the two settles, and in B1. The questions plan's probes and ordered stream, if they run in B0, use locus.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
