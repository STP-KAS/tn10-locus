# Pre-check, the 10-minute freeze

Read 2026-10-09T16:49:36Z. Nothing on the desk was changed for this check. This note does not start a sender or a miner.

## Claim (measured on TN10)

Keel's own log on 9 Oct 2026 shows header IBD that starts, runs, completes, and starts again. Times below are UTC. Duration is from that start to the matching "completed" line.

| Start UTC | Duration |
|---|---|
| 13:57:48 | 653 s |
| 14:08:41 | 660 s |
| 14:19:41 | 645 s |
| 14:30:26 | 650 s |
| 14:41:16 | 655 s |
| 14:52:11 | 648 s |
| 15:02:59 | 656 s |
| 15:13:55 | 658 s |
| 15:24:53 | 438 s |
| 15:32:11 | 247 s |
| 15:36:18 | 97 s |
| 15:37:55 | 57 s |
| 15:38:52 | 19 s |

The first eight sessions are about 11 minutes and sit back to back. That is the whole gap, not a 3–5 minute pause inside a quiet 10 minutes. After 15:38:52 UTC the log has no further IBD start through this read.

At 16:49:36 UTC both desk nodes were testnet-10, kaspad 2.1.0, synced, with the UTXO index on. Locus mempool was 0 and its normal fee was 100 sompi/gram. Its sink lag was 0 s. Keel mempool was 83,165 and its normal fee was 193. Its sink lag was 0 s.

## Not sure / open for debate

The about-650-second cadence is keel's header sync restarting. It is not a Windows task period that matches it.

Enabled or present schedulers near that period: sixpack-faucet-keepalive repeats every 5 minutes and was Ready. GrokBotVprogsWatch repeats every 10 minutes and was Disabled. The node-B watch rewrites its handoff about every 600 seconds and polls about every 60 seconds. 600 seconds is near 650 seconds. It is not the same series.

The pretest sender window ran until 15:30 UTC. The IBD series started at 13:57 UTC, while those senders were up, and the long sessions ended just after 15:30 UTC. Whether those senders caused the restarts is open. No Build sender process was running at 16:43 UTC.

## Nothing found

Locus header-and-block pruning today was one movement, 06:43–07:02 UTC. Not a 10-minute rhythm. Locus IBD starts today were 08:02:17 and 08:02:19 UTC only.

Defender real-time protection was on. The last quick scan was 2026-10-03T17:39:26Z. The last full scan was 2026-02-09T20:38:34Z. No Defender scan was found in the 8 hours before this read.

No Build sender was restarting on a 10-minute clock at this read. The pretest sender tasks were Ready, with last runs earlier in the day. The plan logger task was still running. It does not send.

## Needs more testing

Whether the IBD series returns before 20:15 UTC. The rehearsal still depends on keel lag at 20:15 and at 20:30 UTC. This note does not decide that gate.

## Desk at the same read

NTP, five samples against time.windows.com, 16:44:53–16:45:01 UTC: −209.8 ms, −209.7 ms, −209.7 ms, −209.8 ms, −209.8 ms. This is the start reading. A later move of more than 50 ms flags Build's confirmation times. The absolute offset is not that flag.

Free RAM 8.0 GB of 31.8 GB. Desk disk free 536 GB. Locus process RSS about 2.7 GB. Keel process RSS about 1.6 GB. The 3 Oct halt file on the older fleet still says `halt`.

Twelve locus miners were already up. They stay until 20:30 UTC. No desk miner was on keel at 16:43 UTC.

A read-only coin list at 16:50:25 UTC found 14,883 mature coins of at least 2 tKAS. Locus mempool was still 0, so those coins were not under this desk's own mempool spends. The list stays off git.

## Clock at the end

NTP, five samples against time.windows.com, 2026-10-10 05:01:28–05:01:36 UTC: −215.4 ms, −215.0 ms, −215.8 ms, −214.8 ms, −215.3 ms. The move from the start reading is about 5 ms. Under the 50 ms rule, Build confirmation times stay as recorded.
