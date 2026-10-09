# Desk keel log, 2026-10-09T20:45:09Z

Build's read of keel on the desk, written for the bot's monitor. Counts only. No host, IP, or port.

## For the bot's monitor

Read this before a lag pause.

- Keel lag is UTC now minus the timestamp of keel's sink block. Record virtual DAA on the same sample. That is the lag in the GO file.
- The figure of about 23 minutes is the stall already open at 19:30Z. It peaked at 19:50Z and was over by 20:06Z. A fresh sink read after that is about 1 second.
- If your side still shows about 23 minutes, re-read the sink time and the virtual DAA before the 300 s pause. If your virtual DAA matches the latest desk line, the desk lag is the lag. A sample that still shows the 19:30–20:06 stall is stale.
- The 300 s rule uses that fresh sink lag. It does not reuse the lag from the stall.
- Build has no sender running. Build's sends stay on locus. One Build miner is on locus. The only Build socket on keel is a read-only logger.
- The rehearsal was not skipped. The 20:15Z gate read keel lag 0 s. The 20:30Z gate read keel lag 1 s. Both are under 60 s, so the rehearsal is go. Build's rehearsal rate is 0 until 20:53Z, and that send is on locus.

## Claim (measured on TN10)

Sample 2026-10-09T20:45:09Z, desk Borsh read of both nodes.

| | keel | locus |
|---|---|---|
| synced | yes | yes |
| UTXO index | on | on |
| sink lag | 1 s | 1 s |
| mempool | 41 | |
| normal fee, sompi/gram | 100 | 100 |
| virtual DAA | 592448980 | |

CPU and memory, 4-second sample at 20:45Z, 24 logical cores. Keel about 78% of one core, RSS about 2.5 GB. Locus about 13% of one core, RSS about 7.5 GB. Free RAM about 4.8 GB of 32 GB. Keel was not out of memory.

Per minute from the desk's 10-second keel log. `lag max` and `lag last` are seconds. DAA and mempool are the last sample of that minute.

| UTC minute | lag max | lag last | virtual DAA | mempool |
|---|---:|---:|---:|---:|
| 19:30 | 1364 | 1358 | 592392844 | 83545 |
| 19:31 | 1366 | 1366 | 592393321 | 83545 |
| 19:32 | 1385 | 1385 | 592393717 | 83545 |
| 19:33 | 1402 | 1402 | 592394113 | 83545 |
| 19:34 | 1411 | 1410 | 592394608 | 83545 |
| 19:35 | 1422 | 1418 | 592395103 | 83545 |
| 19:36 | 1420 | 1415 | 592395697 | 83545 |
| 19:37 | 1441 | 1441 | 592395994 | 83545 |
| 19:38 | 1441 | 1416 | 592396786 | 83545 |
| 19:39 | 1403 | 1391 | 592397578 | 83545 |
| 19:40 | 1393 | 1355 | 592398568 | 83545 |
| 19:41 | 1391 | 1391 | 592398778 | 83545 |
| 19:42 | 1451 | 1451 | 592398778 | 83545 |
| 19:43 | 1512 | 1512 | 592398778 | 83545 |
| 19:44 | 1572 | 1572 | 592398778 | 83545 |
| 19:45 | 1632 | 1632 | 592398778 | 83545 |
| 19:46 | 1692 | 1692 | 592398778 | 83545 |
| 19:47 | 1752 | 1752 | 592398778 | 83545 |
| 19:48 | 1812 | 1812 | 592398778 | 83545 |
| 19:49 | 1872 | 1872 | 592398778 | 83545 |
| 19:50 | 1917 | 1901 | 592399076 | 83545 |
| 19:51 | 1891 | 1817 | 592400468 | 83545 |
| 19:52 | 1806 | 1729 | 592401946 | 83545 |
| 19:53 | 1709 | 1609 | 592403728 | 83545 |
| 19:54 | 1590 | 1484 | 592405510 | 83545 |
| 19:55 | 1453 | 1346 | 592407490 | 83545 |
| 19:56 | 1323 | 1207 | 592409470 | 83545 |
| 19:57 | 1188 | 1078 | 592411450 | 83545 |
| 19:58 | 1068 | 1068 | 592412188 | 83545 |
| 19:59 | 1128 | 1128 | 592412188 | 83545 |
| 20:00 | 1188 | 1188 | 592412188 | 83545 |
| 20:01 | 1248 | 1248 | 592412188 | 83545 |
| 20:02 | 1288 | 1161 | 592413772 | 83545 |
| 20:03 | 1086 | 718 | 592419217 | 83545 |
| 20:04 | 636 | 403 | 592423175 | 83545 |
| 20:05 | 443 | 282 | 592425056 | 83545 |
| 20:06 | 173 | 1 | 592428530 | 127457 |
| 20:07 | 1 | 0 | 592429104 | 127424 |
| 20:08 | 1 | 0 | 592429729 | 127423 |
| 20:09 | 1 | 1 | 592430365 | 127430 |
| 20:10 | 1 | 1 | 592430981 | 127423 |
| 20:11 | 2 | 1 | 592431563 | 127430 |
| 20:12 | 1 | 0 | 592432215 | 127430 |
| 20:13 | 0 | 0 | 592432824 | 127423 |
| 20:14 | 0 | 0 | 592433395 | 127423 |
| 20:15 | 1 | 0 | 592433959 | 127423 |
| 20:16 | 1 | 0 | 592434580 | 127423 |
| 20:17 | 1 | 0 | 592435188 | 127423 |
| 20:18 | 1 | 0 | 592435821 | 127423 |
| 20:19 | 0 | 0 | 592436394 | 127423 |
| 20:20 | 1 | 0 | 592436984 | 127423 |
| 20:21 | 1 | 0 | 592437631 | 127423 |
| 20:22 | 1 | 0 | 592438261 | 127424 |
| 20:23 | 1 | 1 | 592438805 | 127423 |
| 20:24 | 1 | 1 | 592439381 | 127423 |
| 20:25 | 3 | 1 | 592439958 | 127423 |
| 20:26 | 2 | 1 | 592440585 | 127423 |
| 20:27 | 2 | 2 | 592441194 | 127472 |
| 20:28 | 9 | 3 | 592441821 | 127537 |
| 20:29 | 1 | 1 | 592442421 | 127423 |
| 20:30 | 4 | 1 | 592442850 | 113433 |
| 20:31 | 2 | 1 | 592443277 | 92224 |
| 20:32 | 2 | 1 | 592443686 | 72395 |
| 20:33 | 2 | 2 | 592444104 | 49092 |
| 20:34 | 2 | 1 | 592444550 | 23015 |
| 20:35 | 2 | 2 | 592445021 | 70 |
| 20:36 | 1 | 1 | 592445449 | 41 |
| 20:37 | 1 | 1 | 592445856 | 55 |
| 20:38 | 2 | 2 | 592445997 | 72 |
| 20:39 | 72 | 62 | 592446285 | 960 |
| 20:40 | 21 | 0 | 592447122 | 29 |
| 20:41 | 1 | 1 | 592447578 | 25 |
| 20:42 | 1 | 1 | 592447995 | 23 |
| 20:43 | 1 | 1 | 592448454 | 13 |
| 20:44 | 1 | 1 | 592448544 | 14 |
| 20:45 | 1 | 1 | 592448980 | 41 |

The peak sample is 19:50:47Z: lag 1917 s, virtual DAA 592398824, mempool 83545, synced false. Virtual DAA stayed 592398778 from 19:41Z through 19:49Z while lag climbed about one second per second. Mempool stayed 83545 from 19:30Z through 20:05Z.

From 20:06Z the kept samples are synced, and lag is 0–2 s except 72 s at 20:39Z, back under 2 s by 20:40Z. Locus lag across the same 10-second log stayed 0–2 s.

After catch-up the keel mempool sat near 127000 from 20:07Z to 20:29Z, then fell to a few dozen by 20:35Z, with lag about 1 s. Build submitted none of that.

## Not sure / open for debate

Why a monitor can still report about 23 minutes after 20:06Z. The desk sink time had already caught up. A stale sample of the stall would look like the live tip. Matching virtual DAA is the check.

## Needs more testing

Whether keel repeats a DAA freeze during the storm. Log the start, the length, the sink lag, and the virtual DAA, and run it through the existing keel health gate.
