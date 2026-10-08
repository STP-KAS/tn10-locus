> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

Wording, Kaspa Pulse (@gokugalax), 7 Oct 2026: sign-and-send processes are senders; runner is the setup; bot is reserved for the operator.

# Prompt for the operator

Paste this into the bot. Sending this GitHub to Grok Build or to the bot means go: start the operation. This file does not lock the questions plan and does not spend.

The bot's runner uses **desk node B**, the second kaspad on the desk, and it runs only during the storm. Build uses locus. If this file and [PLAN.md](PLAN.md) disagree, the plan wins.

## Goal

The highest included tx/s the two sides can hold together. This side's score is transactions desk node B accepted, and only in minutes when node B was synced. Build's node is locus.

## Before any send

Stop unless all three are true:

- This GitHub has been sent to Grok Build or to the bot. That is the storm GO.
- `steps-utc.json` is in hand. Box and Build use the same UTC times.
- The clock is at or after the first time in that file. The runner runs only during the storm.

Then read desk node B. Send only if it is synced and tip lag is at or under 300 seconds. If it is not, sender count stays 0 and the row says `waiting`. Check again on the next 10-minute row. On the desk the runner uses Borsh `ws://127.0.0.1:17310`. From the box it uses the node B tunnel in the desk handoff, after that handoff lists one.

Read free disk before T0. Go only with at least 35 GB free. From 28 to 35 GB, this side's steps shrink to 10 minutes and that is written as a deviation. Below 28 GB, this side does not send. Keep about 19 GB free for pruning on the box. A short box disk does not stop Build.

The hours from 00:25 UTC to 05:30 UTC have no named phase. If the storm GO does not choose, stop and ask.

## This side

- TN10 only. Network `testnet-10`. The Bot wallet only.
- Send through desk node B only. The runner stays off outside the storm.
- Six runners, four connections each, on the paced steps. A seventh only on the max step. Never eight.
- Depth 2. Fee frozen from node B's quote. The pair that held was 200 and 300 sompi/gram, cap 600, unless the questions plan has moved it. If node B's normal quote is already above 200, do not start.
- Point the miners at desk node B. On the desk that is gRPC `127.0.0.1:16310`. Coinbase pays the Grok Bot address `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`. Mine only while node B is synced. Log the count.
- If node B falls behind mid-step, stop the senders.
- `bore.pub` and `159.223.110.159` stay closed.
- Keys stay on the box. Do not print a key, a seed, or a wallet file.

## Logs

Do the bot columns of [MONITOR.md](MONITOR.md), and every bot line in [NEXT-RUN-MONITOR.md](NEXT-RUN-MONITOR.md). Print the 10-minute block for the desk to copy: session, sender count, box disk, NTP, node B synced, lag seconds, node B mempool, node B CPU, submit tx/s, accepted tx/s, rejects, miner count. Per minute the node cell is `desk-nodeB`, or the row is `waiting`. The match is matched over submitted on desk node B. A waiting minute has no match to owe. Five tx ids stay local. A missing block stays **not measured** and fails the bot's part of the pass.

The lane runners stay off outside the storm, and they stay off in B0, in the two settles, and in B1.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
