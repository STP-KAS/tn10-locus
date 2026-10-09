> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for Grok Build

Paste this into Grok Build on the desk. Sending this GitHub to Grok Build or to the bot means go: start the operation. This file does not lock the questions plan and does not spend.

Build uses **locus**, the first desk kaspad. The bot's runner uses keel, the second kaspad on the desk, and it runs only during the storm. If this file and [PLAN.md](PLAN.md) disagree, the plan wins.

## Goal

The highest included tx/s the two sides can hold together. This side's score is transactions locus accepted. The combined score adds the bot's accepted rate. Do not invent the bot's number.

## Before any send

Stop unless all three are true:

- This GitHub has been sent to Grok Build or to the bot. That is the storm GO.
- `steps-utc.json` is in hand.
- The clock is at or after the first time in that file.

Also stop this side unless locus is synced and its UTXO index is on. If desk free RAM is under 1 GB, do not send.

The hours from 00:25 UTC to 05:30 UTC have no named phase. If the storm GO does not choose, stop and ask.

keel's sync is not this side's gate. If the bot's runner is waiting, keep this side on locus. Leave the desk miners on locus while keel is syncing. The bot's miners use the keel tunnel and are not this side's processes.

## This side

- TN10 only. Network `testnet-10`. The Build wallet only.
- Every step goes to locus. Loopback Borsh. Not n0. Not a public node. Not `bore.pub`. Not `159.223.110.159`.
- Four fixed senders on a paced step. Depth 2. In-flight 48. Four connections. No auto-scale.
- Fee frozen from locus's quote at 200 and 300 sompi/gram, cap 600, unless the questions plan has a later long window over 2,207 seen-accepted. If locus's normal quote is already above 200, do not start.
- Leave the 3 Oct halt on the older fleet in place.
- Log the desk miner count. They stay on locus until keel is synced.
- Keys stay on the desk. Do not print a key, a seed, or a wallet file.

## Logs

Do the Build columns of [MONITOR.md](MONITOR.md), and every Build line in [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). Per-transaction logging stays on. Per minute the node cell is `locus`. Five tx ids stay local. The 10-minute row includes locus mempool, the six public pools by name, indexer health, desk disk, free RAM, miner count, submit tx/s, and accepted tx/s. B0 is the first 10 minutes. Send nothing in B0. A blank required line fails the pass.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
