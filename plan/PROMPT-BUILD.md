> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for Grok Build

Paste this into Grok Build on the desk. This file does not start the storm, does not lock the plan, and does not spend.

The node is **locus**, this desk's kaspad. n0 is retired. If this file and [PLAN.md](PLAN.md) disagree, the plan wins. If the plan and the questions repo's `NEXT-STORM-PLAN.md` disagree on a clock, a fee, or a sender count, the questions plan wins.

## Goal

One combo with TN10 ops, on one UTC clock. Friday 9 Oct 2026, 21:30 UTC, for 8 hours, ending Saturday 10 Oct 2026, 05:30 UTC. If that day is not ready, Monday 13 Oct 2026, 21:30 UTC, for 8 hours.

Kaspa Pulse counts Friday 21:25 UTC through Saturday 05:35 UTC. That is his clock. Do not start at 21:00 or at 21:25.

## Before any send

Stop unless all three are true:

- stp has given the storm GO. This file does not give it.
- `steps-utc.json` is in hand. Do not invent the timetable.
- The clock is at or after the first time in that file.

The hours from 00:25 UTC to 05:30 UTC have no named phase. If the storm GO does not name them, or does not end the storm at 00:25, stop and ask.

## This side

- TN10 only. Network `testnet-10`.
- The Build wallet only.
- Every paced step, the long hold, and the max step go to locus. Loopback Borsh. Four fixed senders. Depth 2. In-flight 48. Four connections. No auto-scale.
- Fee frozen at 200 and 300 sompi/gram, cap 600, unless the questions plan has a later long window over 2,207 seen-accepted. If locus's normal quote is already above 200, do not start.
- Do not send to n0, to `bore.pub`, or to `159.223.110.159`.
- Leave the 3 Oct halt on the older fleet in place.
- Log the desk miner count. Do not switch those miners.
- Keys stay on the desk. Do not print a key, a seed, a wallet file, or an address.

## Logs

Per second: sender id, target, submitted, accepted, endpoint, locus mempool. Times are UTC with milliseconds and Z.

Per minute, one local line per sender: minute, sender id, node `locus`, tx_sent, five tx ids spread across the minute. The ids stay local. They do not go in git.

B0 is the first 10 minutes. Send nothing in B0.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
