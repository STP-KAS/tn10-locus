> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Plan

TN10 only. UTC only. This page does not give the storm GO, does not lock the questions plan, and does not start a sender.

The question list, the step table, the fee pair, and the sender counts stay in [NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md). This page replaces the node.

## 1. Locus

**locus** is the desk kaspad.

- Network id `testnet-10`.
- Borsh wRPC is what a sender uses.
- gRPC is what a miner uses.
- UTXO index is on. A sender that cannot read its own mature UTXOs from locus does not send.
- Build, on the desk, uses the loopback Borsh port. TN10 ops, on the box, uses the Borsh URL the desk publishes. Box miners use the gRPC host and port the desk publishes.
- The published host and port are not in git. When the forward drops, the desk publishes the new pair. Runners and box miners move to that pair. They do not guess a host.
- One quote for a step, read from locus at the step start, then frozen.

n0 is out. It is not a fallback. A runner that still has n0 in its URL stops.

Never `bore.pub`. Never `159.223.110.159`.

## 2. Who sends

A process that signs and sends is a sender. The whole setup is a runner. TN10 ops is the operator.

| Side | Wallet | Processes | Where |
|---|---|---|---|
| Grok Build | Build only | 4 fixed senders on the paced steps | locus |
| TN10 ops | Bot only | 6 runners, 4 connections each, on the paced steps | locus |

A seventh box runner only on the max step. Never eight. No auto-scale. No mempool pause inside a step. Each sender spends its own coins. Build does not spend the Bot wallet. TN10 ops does not spend the Build wallet.

Build's share of each paced step stays 25% of the added load, capped at the rate the 6 Oct dry run held. The questions plan is the source of that rate. The box sends the rest. The max step stays uncapped for both, still on locus, still never eight box runners.

Depth 2, in-flight 48, four connections, on a paced step. The questions plan is the source of those three numbers.

Desk miners stay pointed at the desk gRPC. This page does not switch them. Box miners, when they run, use locus gRPC. Log both counts. The miners-off control is still the questions plan's §3b. It switches the miners that are ours. It does not change the node.

## 3. Clock and gate

T0 is Friday 9 Oct 2026, 21:30 UTC, else Monday 13 Oct 2026, 21:30 UTC. First load step 21:40 UTC. End 05:30 UTC the next morning. Paced table ends 00:25 UTC. The hours from 00:25 to 05:30 have no name until the storm GO names them, or ends the storm at 00:25. This page does not choose.

Before any send, all three:

1. A storm GO from stp. A dry-run GO is not this.
2. `steps-utc.json`, with a UTC start and a UTC end for every step. Do not invent the table.
3. The clock is at or after the first time in that file.

B0 is the first 10 minutes. Lane senders stay off. The questions plan still keeps the box probes and the box ordered stream in B0. Those probes now read locus, not n0. Build still sends nothing in B0.

### Retired with n0

These stop being gates:

- n0 synced, or n0 lag at or under 300 seconds.
- n0 match of transaction ids.
- 35 GB free on the box disk, the 28 GB shrink, and the 19 GB pruning reserve. Those numbers were the n0 disk. The questions plan's §9 describes that box. It is not locus.

### Still open

- Storm GO.
- `steps-utc.json`.
- The questions plan is still unlocked. At T0 the run log writes the SHA of the last commit that changed `plan/NEXT-STORM-PLAN.md`, and the SHA of this repo's `plan/PLAN.md`.
- A sender dry run against locus, if the storm GO does not name it as left open.
- The unnamed hours after 00:25 UTC.

## 4. Fees

The pair stays **200 and 300** sompi/gram, cap **600**, until a multi-hour seen-accepted rate over **2,207** is written into the questions plan. That 2,207 is the questions plan's long number, not a new measurement here.

At each step start, read locus. Freeze F1 and F1.5 for the step. Half the lanes at each tier. If locus's normal quote is already above 200, do not start that step. Ask stp.

## 5. What locus is not

n0 ran with `--ram-scale=0.1`, no UTXO index, and a mempool cap near 100,000 transactions. That reading is the questions plan's §6a, from Monday 5 Oct 2026. It does not describe locus.

Locus runs with a UTXO index and without `--ram-scale`. Its mempool cap is the node's own default, not the 100,000 figure. Log the flags at T0 from the running process. Do not copy n0's cap into the label rules.

On 8 Oct 2026 the desk was 16 cores and about 32 GB of RAM, with this kaspad, the desk miners, and the senders on one machine. Ten sender processes were the largest set that stayed up. That set also faulted the node. Four Build senders plus six box runners is ten processes on locus. Do not add an eighth box runner to get past a fault. If locus dies, or desk free RAM falls under 1 GB, both sides stop. That stop is the run. It is written down. It is not a cue to relaunch a larger set.

Block mass still tops out near 305 transactions in a block, about 3,024 included tx/s for a transaction near 1,624 grams, at 10 blocks per second. That ceiling is the questions plan's mass note. Locus does not raise it. A fat mempool with orphans, while locus is synced, is that cap until the logs say otherwise.

## 6. Acceptance

Both sides read acceptance from locus. A submit acknowledgement is the other counter. Kaspa Pulse counts the chain. His count and the locus count stay two numbers until the same ids are on both clocks. Comparison comes to this side first. This page does not ping him.

The id match is **locus match**: ids this node accepted, over ids submitted. The old n0 match is closed as a gate because n0 is retired. Historical ids that were only checked against n0 stay in the old repos. They are not reopened here.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
