> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for the operator

Paste this into TN10 ops on the box. This file does not start the storm, does not lock the plan, and does not spend.

The bot uses **n0** when n0 is synced. Build uses its own node. If this file and [PLAN.md](PLAN.md) disagree, the plan wins.

## Goal

The highest included tx/s the two sides can hold together. This side's score is transactions n0 accepted, and only in minutes when n0 was synced. Do not send through Build's node to chase the combined number.

## Before any send

Stop unless all three are true:

- stp has given the storm GO. This file does not give it.
- `steps-utc.json` is in hand. Box and Build use the same UTC times.
- The clock is at or after the first time in that file.

Then read n0. Send only if it is synced and tip lag is at or under 300 seconds. If it is not, sender count stays 0 and the row says `waiting`. Check again on the next 10-minute row. Do not point the runners at the desk.

Read free disk before T0. Go only with at least 35 GB free. From 28 to 35 GB, this side's steps shrink to 10 minutes and that is written as a deviation. Below 28 GB, this side does not send. Keep about 19 GB free for n0 pruning. A short box disk does not stop Build.

The hours from 00:25 UTC to 05:30 UTC have no named phase. If the storm GO does not choose, stop and ask.

## This side

- TN10 only. Network `testnet-10`. The Bot wallet only.
- Send through n0 only. Do not send to locus, to a public signer, to `bore.pub`, or to `159.223.110.159`.
- Six runners, four connections each, on the paced steps. A seventh only on the max step. Never eight.
- Depth 2. Fee frozen from n0's quote. The pair that held was 200 and 300 sompi/gram, cap 600, unless the questions plan has moved it. If n0's normal quote is already above 200, do not start.
- Box miners stay on n0. Log the count. Do not point them at the desk.
- If n0 falls behind mid-step, stop the senders. Do not fail over.
- Keys stay on the box. Do not print a key, a seed, a wallet file, or an address.

## Logs

Do the bot columns of [MONITOR.md](MONITOR.md), and every bot line in [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). Print the 10-minute block for the desk to copy: session, sender count, box disk, NTP, n0 synced, lag seconds, n0 mempool, n0 CPU, submit tx/s, accepted tx/s, rejects, miner count. Per minute the node cell is `n0`, or the row is `waiting`. The match is matched over submitted on n0. A waiting minute has no match to owe. Five tx ids stay local. A missing block stays **not measured** and fails the bot's part of the pass.

The lane runners stay off in B0, in the two settles, and in B1.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
