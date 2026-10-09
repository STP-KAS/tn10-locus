> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Rehearsal, 9 Oct 2026, before T0

TN10 only. Every clock time is UTC. stp approved this rehearsal on 9 Oct 2026 at 16:08 UTC. It is linked from [PLAN.md](PLAN.md). If this page and the plan disagree on anything but the rehearsal itself, the plan wins.

The rehearsal is not the storm. It does not move T0, it is not the storm GO, and it does not change the GO rules. T0 stays Friday 9 Oct 2026, 21:00 UTC. stp's 16:08 UTC approval is the one exception to "the runner runs only during the storm", and only for the 30 minutes below.

## When

- 30 minutes, once, at a fixed time: R = 20:30 UTC, ending 21:00 UTC. Both sides use the same clock without talking to each other.
- It runs only if keel is synced and its lag is at or under 60 seconds at 20:15 UTC (T0 − 45) and again at 20:30 UTC. Keel lag = UTC now − timestamp of keel's sink block.
- If not, the rehearsal is skipped. The log writes **not run**, with the last keel lag and the UTC of that read. A skipped rehearsal is not a failed storm gate. The miners still start at 20:30 UTC.
- Every step below is R + minutes. The launch files [GO-BOT.md](GO-BOT.md) and [GO-BUILD.md](GO-BUILD.md) print the same steps in UTC.

## Rules

- Same split as tonight. The bot sends to keel only and runs 1 miner on keel only. Build sends to locus only and runs 1 miner on locus only. No desk miner on keel. No bot miner on locus.
- Keel health gate, the whole time: lag over 120 seconds halves the bot's rate; over 300 seconds stops the bot's senders and the bot's miner. A freeze (below) stops the bot's senders for the rest of the rehearsal. Build is not stopped by keel.
- Fixed rates inside each step. No auto-scale.
- Fees as [PLAN.md](PLAN.md) §4 has them: each side's own live normal quote at 1× and 1.5×, the 200 and 300 pair, cap 600, frozen at R.
- No txid, key, IP or tunnel host in git. Ids stay in the local log. Git gets counts.

## Steps

| # | R + min | What | Bot | Build | Pass |
|---|---|---|---|---|---|
| 1 | 0–30 | keel health, and the 10-minute freeze watch | reads keel every 10 s: synced, lag, DAA score, mempool; public-node DAA every 60 s | desk CPU, RAM and disk for keel and locus every minute | synced the whole time, lag ≤ 60 s on every read, and no freeze. A freeze is keel's DAA score not moving for 60 seconds or more while the public node moves. |
| 2 | 0–30 | Miner split live | 1 miner (box CPU `kaspa-miner`, 1 thread) on keel through the keel tunnel, paying `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`, user agent suffix `stp grok bot` | 1 miner on locus | Each miner finds at least 1 block that its own node accepts. Mining share per node is written: blocks total, blocks ours, percent, on the blocks keel sees and on the blocks locus sees. A miner with 0 blocks is **fail: no block**. |
| 3 | 0–10 | Bot runners at 60 tx/s | 60 tx/s on keel, fixed, up to 15 runners | 0 | Eventual accept ≥ 99%, p90 submit-to-accept ≤ 10 s, keel lag ≤ 60 s, rejects 0 outside tunnel events. |
| 4 | 10–20 | Light-tx lane | runners 0; light lane at 20 tx/s for 5 min, then 50 tx/s for 5 min | 0 | Keel takes every hop into its mempool, with no reject. At least 99% of each half's ids are in keel's `getVirtualChainFromBlock` `acceptedTransactionIds` within 2 minutes of that half's end. p90 ≤ 10 s. The 50 tx/s half runs only if the 20 tx/s half passed. |
| 5 | 20–29 | Duplicate-share sample | 60 tx/s, then 0, then 60 tx/s | 0, then 60 tx/s, then 60 tx/s | Each 3-minute block has a reading: tx slots/s in blocks, unique ids/s, duplicate share = 1 − unique/slots, and unique accepted/s from `acceptedTransactionIds`. Order: Bot only (3 min), Build only (3 min), both (3 min). |
| — | 29–30 | Wrap | runners 0, miner stays on | senders 0, miner stays on | The rehearsal block is printed. |

Build's fixed rate in step 5 is 60 tx/s, the same as the bot and the same as the storm's one-side control.

**Light lane.** P2SH with redeem script `OP_TRUE`. Each hop is 1 input, 1 output, unsigned, 637 mass. Today's 13:47 UTC probe found it standard-valid on keel: a fund transaction of 1,701 mass and 3 hops of 637 mass, all accepted into keel's mempool. Small amounts only, from a pre-split fund. Every light-lane number carries the label **anyone-can-spend hops, not realistic payments**.

**Duplicate share.** The method is the one from today's report: keel's `block-added` full blocks against the transactions keel's virtual chain accepted. A 3-minute block is a sample. **Needs more testing.** It does not settle the split.

## Output

One rehearsal block, printed for the desk and kept with tonight's logs:

- R, the end time, or **not run** with the reason.
- For each step: pass, fail, or not run, with the numbers behind it.
- keel lag max, freezes (count, start UTC, length), public-node DAA per second.
- Mining share per node.
- Light lane: sent, in mempool, in `acceptedTransactionIds`, p50 and p90, with its label.
- Duplicate share and unique accepted/s for the three blocks of step 5.

## What a result changes

- Step 1 fails: the bot keeps the keel health gate at T0. The bot side may sit at 0 tonight. Build is not stopped.
- Step 3 fails: the bot starts the storm at 30 tx/s instead of 60, and writes that as a deviation.
- Step 4 fails: the light lane stays off in the storm.
- Step 2 or step 5 fails: written as found. The storm's one-side control still runs.

## Labels

- **Claim (measured on TN10):** the light hop is standard-valid on keel (13:47 UTC probe). 60 tx/s held clean on keel today.
- **Not sure / open for debate:** whether one miner per node, mining where its own side sends, lowers the duplicate share.
- **Needs more testing:** the light lane at 20 and 50 tx/s, and its on-chain inclusion. The duplicate share per side.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
