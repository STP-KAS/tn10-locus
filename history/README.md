> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# History: the TN10 stress tests, the longer map

Kaspa Testnet-10 only. Clocks are UTC unless marked otherwise; older repos often write CEST (UTC+2), and the times below were converted. Every number names the repo it comes from. A number is labelled as in the [README](../README.md#how). The short map is in the [README](../README.md#map-of-related-repos).

Counters differ between eras, so numbers are not directly comparable:

- **Processed**: kaspad's block-body counter. Counts every sender, and copies in parallel blocks.
- **Included / seen-accepted**: a sender saw its own transaction on a node's virtual chain.
- **Submit-OK**: the node took the transaction into its mempool. Not inclusion.
- **Unique accepted**: each id once, when the virtual chain accepts it. This is the score now.

## Timeline

### Mid September: first contact

- **14 Sep.** Grok Build's catalog of every STP-KAS repo tested against groks-wallet on TN10. [tn10-hard-test](https://github.com/STP-KAS/tn10-hard-test).
- **18–21 Sep. Farm mining stress.** A dedicated TN10 kaspad with up to 150 one-thread CPU miners. **Claim (measured on TN10):** IBD stuck near 99% headers on one peer, `RouteIsFull` on block submits under farm load, one datadir lock panic. [tn10-grok](https://github.com/STP-KAS/tn10-grok) (private); summary in the public report's [mainnet-implications note](https://github.com/STP-KAS/tn10-storm-2026-10-public-report/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md) §1.

### 25–26 Sep: the September storm, with vprogs

- **25 Sep, break test (round 1 overload).** The box node n0 alone, small mempool cap. **Claim (measured on TN10):** the Processed counter averaged 6,466 tx/s (10-s peak 9,274); mempool hit about 100k with 30,298 fee evictions. Source: the break-test findings, cited in the mainnet-implications note §2. The break-test folder is not on GitHub.
- **25 Sep, 19:55:38 UTC.** The public api-tn10 indexer stopped advancing accepted transactions during our storm and still returned HTTP 503 on 29 Sep (at least 3 days 15 hours). **Not sure / open for debate:** whether our load caused it; time correlation is not causation. [tn10-indexer-stall-2026-09](https://github.com/STP-KAS/tn10-indexer-stall-2026-09) (private).
- **25–26 Sep, rounds 2–6.** About 17 hours of load while running vprogs and the vprog tic-tac-toe. **Claim (measured on TN10):** round 4 held 1,219 accepted tx/s for 1 h 32 min; round 6 got 10,058,024 accepted in about 159 min. Round 7 measured three counters side by side: 267.2/s unique selected-chain accepted against 357.2/s Processed, so Processed overstates unique throughput. The vprogs PR #165 author mapped every finding upstream. [tn10-vprogs-stress-findings](https://github.com/STP-KAS/tn10-vprogs-stress-findings), [round 2](https://github.com/STP-KAS/grok-bot-vprogs-round2) … [round 6](https://github.com/STP-KAS/grok-bot-vprogs-round6), [tn10-vprogs-round7-ideas](https://github.com/STP-KAS/tn10-vprogs-round7-ideas), [tn10-vprogs-final-verdict](https://github.com/STP-KAS/tn10-vprogs-final-verdict).
- **26 Sep–3 Oct.** Pruning disk spikes and resyncs on n0 (temporary disk 11–15 GB; a disk-full crash on 3 Oct). This is why later plans carry disk guards. Mainnet-implications note §6.
- **27 Sep.** The desk's CPU miners were set up against our TN10 node. [grok-desk-tn10](https://github.com/STP-KAS/grok-desk-tn10) (private).

### 1–4 Oct: the box storm

- **1–3 Oct, legs L1–L4.** Index-free runners on n0, Build adding load from the desk through public nodes. **Claim (measured on TN10):** 58,905,910 box transactions included in four legs, 152 rejected; best 1 minute 4,253 tx/s, best 10 minutes 3,717, best 60 minutes 2,518. Our block share was 50–63% while the box miners ran. The public API lagged up to 11.7 min and froze about 85 min on the night of 2 Oct, and each episode we saw end recovered within 2–5 min. **Not sure / open for debate:** "~5k TPS" does not hold as unique included transactions. [tn10-storm-2026-10-public-report](https://github.com/STP-KAS/tn10-storm-2026-10-public-report); raw data and Build's analysis in [tn10-storm-2026-10-analysis](https://github.com/STP-KAS/tn10-storm-2026-10-analysis) (private); the box report copy in [tn10-stress-tests](https://github.com/STP-KAS/tn10-stress-tests) (private).
- **1–2 Oct, "full gusto".** Desk spend ramps on one public node, avoiding public nodes whose mempools were over 100k. [tn10-gusto-20261002](https://github.com/STP-KAS/tn10-gusto-20261002), [tn10-gusto-ledger](https://github.com/STP-KAS/tn10-gusto-ledger), [tn10-full-gusto](https://github.com/STP-KAS/tn10-full-gusto) (all private).
- **4 Oct.** Every mainnet sentence got an A/B/C label (shown on TN10 / plausible / unknown) in the [mainnet-implications note](https://github.com/STP-KAS/tn10-storm-2026-10-public-report/blob/main/TN10-STORMS-MAINNET-IMPLICATIONS-2026-10-04.md). Kaspa Pulse's questions arrive by X DM; [tn10-storm-throughput-questions](https://github.com/STP-KAS/tn10-storm-throughput-questions) starts.

### 5–7 Oct: method first, and the mass ceiling

- **5 Oct.** Kaspa Pulse reviews the draft plan: four tightenings. The plan is rewritten around his questions ([NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md)).
- **6–7 Oct, Build's desk runs via public nodes.** **Claim (measured on TN10):** 6,321 tx/s submit-OK for 20 s, with about 1,900/s seen accepted in the same window, so the 6,321 is submit, not inclusion. A 6-hour hold of 2,207 seen-accepted tx/s, 6 Oct 23:53 to 7 Oct 05:54 UTC, at fee 200/300. [tn10-build-desk-tps](https://github.com/STP-KAS/tn10-build-desk-tps). The challenge repo [tn10-storm-build-bot-challenge](https://github.com/STP-KAS/tn10-storm-build-bot-challenge) opens, empty until the storm.
- **7 Oct, the ceiling.** **Claim (measured on TN10):** full blocks of about 304–307 signed payments, compute mass about 497,000–498,800 of 500,000, near 3,040–3,070 tx/s for the network. A signed 1-in/1-out is about 1,624 mass, so about 3,080 tx/s is the ceiling for that shape; an unsigned anyone-can-spend hop at 643 mass would allow about 7,780. 3,500 included was not reached. [what-limits-tx-rate](https://github.com/STP-KAS/what-limits-tx-rate), [tn10-build-desk-tps-3500](https://github.com/STP-KAS/tn10-build-desk-tps-3500).
- **7 Oct, the Pulse window.** His chain count for 18:52–19:23 UTC came out much lower than our screenshot. Our desk log had stopped at 18:38:39 UTC, so the windows did not overlap, and the 2,750 figure and the ~9.7k pool were readings from other minutes. Lesson: one window, one clock, sent and accepted kept apart. [PULSE-WINDOW-7-OCT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/PULSE-WINDOW-7-OCT.md).
- **7 Oct.** The combo hub [grok-bot-build-combo](https://github.com/STP-KAS/grok-bot-build-combo) is set up. The storm is set for Fri 9 Oct, 8 hours from 21:30 UTC, with Mon 13 Oct as fallback.

### 8 Oct: the checkout, and n0 retired

- **18:00–20:11 UTC, desk checkout on locus.** Ten rounds. **Claim (measured on TN10):** six senders held 2,191 submit / 2,143 local accept tx/s; ten held 2,100 / 1,954. More senders added waiting hops, not throughput. Eleven or more exhausted desk RAM. locus exited twice (19:00:06 and 19:03:41 UTC) and was restarted. The bot side was not measured because n0 was still syncing. [AFTER-8-OCT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/AFTER-8-OCT.md), [tonight-8-oct/RESULTS.md](https://github.com/STP-KAS/grok-bot-build-combo/blob/main/tonight-8-oct/RESULTS.md).
- **Evening.** The desk node is named locus and this repo starts. n0 is retired (finalized the next morning).

### 9 Oct: keel pre-test and the duplicate finding

- **Morning.** The second desk node is named keel; the bot reaches it through a tunnel.
- **09:37–13:30 UTC, keel runs 1–5.** Bot runners on keel, light 643-mass hops, fee 200/300. **Claim (measured on TN10):** 15 runners held 60 tx/s with 100% eventually accepted; 100 tx/s was accepted but failed the p90 ≤ 10 s rule; run 5 ended on the keel lag rule (302 s). [monitoring-result/bot-result](../monitoring-result/bot-result/README.md).
- **Duplicates.** **Claim (measured on TN10):** 48–49% of tx slots in blocks were copies of a transaction already in another block (12:29 and 12:55 UTC); transactions only in red blocks were accepted. Unique accepted while keel kept up: average 1,627 tx/s, max 2,435. Build's 12:23 UTC desk window (3,611/s into blocks, 2,371/s unique) fits the same reading, and Build dropped its "off-chain blocks never join" claim. [build-result](../monitoring-result/build-result/README.md), [goal/OPINION.md](../goal/OPINION.md).
- **Afternoon.** With no bot load, keel fell up to 868 s behind the public node (which averaged 9.64 DAA/s) and froze 3–5 min about every 10 min from about 14:05 UTC. **Needs more testing:** cause not found; Build's pre-check covers it ([GO-BUILD.md](../go/build/GO-BUILD.md)).
- **What changed for tonight, and why.** One miner per side on its own node (to test whether duplicates drop); a one-side control (bot alone, Build alone, both) to split the duplicate share; a keel health gate and a 30-minute rehearsal; Build stops other senders so the baseline means something; T0 moved to 21:00 UTC; the hours after 00:25 named (long hold, drain), which answers Pulse's 8 Oct question; two GO files locked with one UTC/Brussels table. [plan/PLAN.md](../plan/PLAN.md), [go/](../go/bot/GO-BOT.md).

## Credit: Kaspa Pulse, in full

Kaspa Pulse ([@gokugalax](https://x.com/gokugalax)), X DMs from 4 Oct 2026. He stays out of the setup, counts what the chain accepted from outside it, and sends his comparison first. Each line below is what the repos record, with the file.

| Contribution | Date | Where it is recorded |
|---|---|---|
| **Five questions**: accepted vs submitted and where it flattens; confirmation time per step, 1× vs 1.5×; indexer freeze; mempool depth; send order vs accept order | 4–7 Oct | [plan/PULSE-README.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/PULSE-README.md) §Questions; [NEXT-STORM-PLAN.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/NEXT-STORM-PLAN.md) "What" table; [tn10-storm-build-bot-challenge](https://github.com/STP-KAS/tn10-storm-build-bot-challenge) README |
| **Six method points**: plan written first and published with its commit SHA and a deviations list; 10-minute baseline first; fixed load steps (his example 1×, 2×, 5×, 10×), not one blast; submitted and accepted per second in UTC with send vs accept order; mining share stated up front; raw data next to the summary | 4–7 Oct | PULSE-README.md §Method; NEXT-STORM-PLAN.md §1–§4, §7, §8 ("Kaspa Pulse's six process points") |
| **Four tightenings**: miners-off control in the main run at low load, matched to a miners-on step, called imperfect; box vs network: log node CPU, cap hits and reject reasons, label each plateau box-bound or network-bound; NTP on box and desk, offsets at start and end; saturation defined before T0 (accepted < 95% of submitted for 60 s), reorder rates as counts and percentages with n, probe sample raised from ~90 to ~450 per tier per step | 5 Oct | NEXT-STORM-PLAN.md "Kaspa Pulse's four tightenings"; PULSE-README.md §Four tightenings. The questions README notes his 5 Oct 15:01 UTC message was cut at "Show more"; the plan's table is the working copy |
| **Counting the chain from outside**, side by side after the run, comparison sent to us first | 7–9 Oct | PULSE-README.md §Dry-run compare; [tonight-8-oct/PULSE.md](https://github.com/STP-KAS/grok-bot-build-combo/blob/main/tonight-8-oct/PULSE.md); [monitoring-result/README.md](../monitoring-result/README.md) |
| **The 7 Oct window check**: one window and transaction ids on both clocks; the 2,750 figure and the ~9.7k pool named chain or node before anyone calls them a ceiling | 7 Oct | [PULSE-WINDOW-7-OCT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/PULSE-WINDOW-7-OCT.md) |
| **Cadence**: "one clean run first", read the numbers, then weekly | 7 Oct | NEXT-STORM-PLAN.md (quoted at the top) |
| **Wording**: senders sign and send, runner is the setup, bot is the operator | 7 Oct | The wording line on every page of this repo and of the questions repo |
| **Checkout read**: per-minute sent count, node by name, five ids per minute (ids kept local); flagged that the hours after 00:25 UTC had no named phase | 8 Oct | tonight-8-oct/PULSE.md; [AFTER-8-OCT.md](https://github.com/STP-KAS/tn10-storm-throughput-questions/blob/main/plan/AFTER-8-OCT.md) §1, §3 |
| **9 Oct first look**: our rounds line up with his minutes; keep the desk node's accept and his block count apart | 9 Oct | tonight-8-oct/PULSE.md "9 Oct 2026" |
| **Scope**: deliberate load stays on TN10; mainnet comparisons and costing out of scope, as he asked | 4–7 Oct | NEXT-STORM-PLAN.md header |
| **Offer**: to be the independent side of a possible later open builder leg (not planned) | 7 Oct | NEXT-STORM-PLAN.md §10 |

His Friday counter runs 21:25 UTC to Saturday 05:35 UTC (combo PULSE.md, AFTER-8-OCT.md). It was set around the old 21:30 T0.

## Older clocks and rules that no longer apply

- **n0 routing** (questions plan §6a, §9, combo root prompts): n0 does not run.
- **T0 21:30 UTC, end 05:30, Monday 13 Oct fallback** (questions repo, combo hub, challenge repo): tonight is 21:00–05:00 UTC, no fallback.
- **Build through public nodes, four fixed senders, 25% share** (questions README): tonight Build sends on locus only, per GO-BUILD.md.
- **"Off-chain blocks never join the accepted set"**: withdrawn on 9 Oct.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
