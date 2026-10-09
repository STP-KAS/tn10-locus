> **Experimental. We are just trying this.** See [DISCLAIMER](../../DISCLAIMER.md).

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Build result

Every clock time in this repo is UTC.

This folder is Build's monitor. The desk measured locus. These numbers are not the bot's keel rates in [bot-result](../bot-result/README.md). The questions being counted are Kaspa Pulse's ([@gokugalax](https://x.com/gokugalax)). The plan stays at [plan/](../../plan/PLAN.md).

## 8 Oct

The desk sheet is [tonight-8-oct/RESULTS.md](https://github.com/STP-KAS/grok-bot-build-combo/blob/main/tonight-8-oct/RESULTS.md). Accepted in that sheet is what locus took. It is not the bot's accept count.

## 9 Oct, 12:23:20Z, 15.02 seconds, on the synced desk node

**Claim (measured on TN10).** 54,242 transactions were written into blocks, 3,611/s. Unique accepted was 35,611, 2,371/s. DAG blocks were 172 (11.45/s). Selected-chain blocks were 79 (5.26/s). The other 93 blocks were not on the selected chain.

**Claim (measured on TN10).** The keel minute that starts at 12:23:30Z, in the bot's file `network-tps-1m.csv`, is 2,045 accepted/s over 63.3 s. The 2,371/s figure is this short desk window, not that minute.

The sentence that those off-chain blocks never joined the accepted set does not hold. The bot's colored windows show transactions that appeared only in red blocks were accepted. That reading is in [bot-result](../bot-result/README.md), section "Block redundancy". Build's change of view is: the gap is duplicate transactions across parallel blocks, not lost off-chain transactions.

The full 9 Oct sender log from the desk is not in this folder. The lines Build still has to fill are [MONITOR.md](../../plan/MONITOR.md) and [NEXT-RUN-MONITOR.md](../../plan/NEXT-RUN-MONITOR.md).
