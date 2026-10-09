> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for the operator

For tonight, paste [GO-BOT.md](../go/bot/GO-BOT.md) instead. It is the launch file. This page is the standing prompt. Paste this into the bot. Sending this GitHub to Grok Build or to the bot means go: start the operation. This file does not lock the questions plan and does not spend.

The bot's runner uses **keel**, the second kaspad on the desk, and it runs only during the storm and the rehearsal. Build uses locus. Each side mines where it sends: one bot miner on keel, one Build miner on locus. If this file and [PLAN.md](PLAN.md) disagree, the plan wins.

## Goal

The highest included tx/s the two sides can hold together. This side's score is transactions keel accepted, and only in minutes when keel was synced. Build's node is locus.

## Before any send

Stop unless all three are true:

- This GitHub has been sent to Grok Build or to the bot. That is the storm GO.
- `steps-utc.json` is in hand. Box and Build use the same UTC times.
- The clock is at or after the first time in that file. The runner runs only during the storm.

n0 will not run. Do not start it. This side uses the tunnel to keel. Then read keel. Send only if it is synced, the handoff lists the tunnel, and tip lag is at or under 60 seconds. If not, sender count stays 0 and the row says `waiting`. Check again on the next 10-minute row. Do not use `ws://127.0.0.1:17310` from this box. Do not invent a host.

Read free disk before T0. Go only with at least 35 GB free. From 28 to 35 GB, this side's steps shrink to 10 minutes and that is written as a deviation. Below 28 GB, this side does not send. Do not keep disk aside for n0 pruning. A short box disk does not stop Build.

**Rehearsal.** Before T0, run [REHEARSAL-2026-10-09.md](REHEARSAL-2026-10-09.md) once keel's lag is at or under 60 seconds. If keel is not healthy by 20:15 UTC, write **not run** and skip it.

The hours after 00:25 UTC are named in [GO-BOT.md](../go/bot/GO-BOT.md): long hold to 04:45 UTC, final drain to 05:00 UTC.

## This side

- TN10 only. Network `testnet-10`. The Bot wallet only.
- Send through the keel tunnel only. Never to locus. The runner stays off outside the storm and the rehearsal. n0 stays off.
- One-side control after B0: 21:10–21:20 UTC this side alone at 60 tx/s, 21:20–21:30 UTC this side at 0 (Build alone at 60), 21:30–21:40 UTC both at 60 tx/s each. Then the paced steps.
- Start at 60 tx/s. Step up only at a step boundary, and only while the last step had eventual accept ≥ 99%, p90 ≤ 10 s and keel lag ≤ 60 s. Up to 15 runners, four connections each.
- Keel health gate: lag over 120 seconds, halve; over 300 seconds, stop; resume at the halved rate once lag is back at or under 60 seconds.
- Depth 2. Fee frozen from keel's quote. The pair that held was 200 and 300 sompi/gram, cap 600, unless the questions plan has moved it. If keel's normal quote is already above 200, do not start. A higher fee reorders. It does not add capacity.
- Exactly 1 miner: box CPU `kaspa-miner`, 1 thread, on the keel tunnel, gRPC host and port from the handoff. Coinbase pays the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`. User agent suffix `stp grok bot`. Mine only while keel is synced and the handoff lists the tunnel. Until then it stays off. Not on locus, not on n0. Log the count.
- Optional light lane: P2SH `OP_TRUE`, 637 mass, small amounts, only while keel passes the gate and only if the rehearsal's light step passed. Label every number **anyone-can-spend hops, not realistic payments**.
- `bore.pub` and `159.223.110.159` stay closed.
- Keys stay on the box. Do not print a key, a seed, or a wallet file.

## Logs

Do the bot columns of [MONITOR.md](MONITOR.md), and every bot line in [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). Print the 10-minute block for the desk to copy: session, sender count, box disk, NTP, keel synced, lag seconds, keel mempool, keel CPU, submit tx/s, accepted tx/s, rejects, miner count, keel DAA/s next to the public node's, freezes, and the duplicate share (tx slots/s, unique/s, unique accepted/s). Per minute the node cell is `keel`, or the row is `waiting`. The match is matched over submitted on keel. A waiting minute has no match to owe. Five tx ids stay local. A missing block stays **not measured** and fails the bot's part of the pass.

The lane runners stay off outside the storm, and they stay off in B0, in the two settles, and in B1.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
