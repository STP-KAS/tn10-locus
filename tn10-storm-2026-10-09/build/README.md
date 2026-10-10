# Build result, TN10 storm, 9 Oct 2026

Counts only. The clock was `steps-utc.json`. The pre-check is `precheck.md`. Per-minute locus chain counts are `chain-minute.csv`.

GO file `2673e02f4ed4cadf11b8a73ba6653c51b7c0762c`. Questions plan `fc9558e306cdea34de0234968d7c3c1e974cdcc4`.

## How a rate is counted

The headline is network unique accepted tx/s, counted once, from locus chain data when the minute is valid. A minute is valid when locus stayed synced, its lag stayed at or under 60 s on the samples in that minute, and it accepted at least 95% of the unique ids it saw in blocks. Keel's accepted count is not added. The bot writes `COMBINED.md` and may use keel for a minute locus did not validate.

Build submitted and Build accepted are attribution for this wallet's own ids. Shape: **signed payment**, mass about 1,624. Slots are not tx/s. A signed-payment number is not taken from a mixed total.

Tonight's signed share (these senders, the probes, and the ordered stream) was planned well under about 3,080 tx/s. Tonight cannot show whether signed payments reach 3,080. 3,500 signed payments do not fit in the block mass and are not a target.

A step headline is the median of valid minutes in the load window. Drains are outside that window. Under 5 valid minutes: not enough data. A single minute at or over 3,000 is a peak, not the goal. The goal line wants a step median at or over 3,000 with at least 10 valid minutes.

## Step table

| Phase | Load window | Valid minutes | Headline unique accepted tx/s | Peak minute | Own accepted tx/s (signed payment, ~1624 mass) | Duplicate share | Own-id duplicate share | Own eventual accept % |
|---|---|---|---|---|---|---|---|---|
| stop-and-health | 20:15–20:30 | 15/15 | 60.72 | 64.26 | 0 | 0.31 | 0 | not measured |
| rehearsal-miners | 20:30–20:53 | 21/23 | 112.74 | 119.66 | 0 | 0.41 | 0 | not measured |
| rehearsal-60 | 20:53–20:59 | 6/6 | 149.19 | 186.88 | 59.45 | 0.42 | 0.43 | 99.7 |
| rehearsal-wrap | 20:59–21:00 | 1/1 | not enough data | 63.13 | not measured | 0.35 | 0 | not measured |
| B0 | 21:00–21:10 | 10/10 | 64.59 | 66.39 | 0 | 0.38 | 0 | not measured |
| C1 | 21:10–21:20 | 10/10 | 73.7 | 76.2 | 0 | 0.3 | 0 | not measured |
| C2 | 21:20–21:30 | 10/10 | 59.62 | 68.73 | 0 | 0.34 | 0 | 0 |
| C3 | 21:30–21:40 | 6/11 | 59.22 | 61.28 | 0 | 0.36 | 0 | 0 |
| 2x | 21:40–21:55 | 15/15 | 59.79 | 66.7 | 0 | 0.33 | 0 | 98.47 |
| settle-off | 22:00–22:05 | 5/5 | 103.49 | 105.57 | 0 | 0.31 | 0 | not measured |
| 2x-miners-off | 22:05–22:20 | 15/15 | 66.57 | 110.81 | 6.88 | 0.34 | 0.23 | 99.98 |
| settle-on | 22:25–22:30 | 5/5 | 103.18 | 105.98 | 0 | 0.36 | 0 | not measured |
| 5x | 22:30–22:45 | 15/15 | 213.68 | 260.69 | 145.55 | 0.27 | 0.21 | 99.88 |
| 10x | 22:50–23:05 | 15/15 | 428.4 | 470.74 | 356.98 | 0.25 | 0.22 | 99.93 |
| 20x | 23:10–23:25 | 15/15 | 888.81 | 904.01 | 779.65 | 0.3 | 0.28 | 99.94 |
| 30x | 23:30–23:45 | 15/15 | 1078.3 | 1089.72 | 966.79 | 0.32 | 0.32 | 99.92 |
| max | 23:50–00:05 | 15/15 | 67.03 | 111.66 | 0 | 0.35 | 0 | not measured |
| B1 | 00:15–00:25 | 10/10 | 111.13 | 155.08 | 0 | 0.34 | 0 | not measured |
| hold | 00:25–04:45 | 63/260 | 1039.78 | 1233.51 | 969.85 | 0.31 | 0.3 | 1.39 |
| final-drain | 04:45–05:00 | 0/14 | not enough data | 0 | not measured | not measured | not measured | 0 |
| end | 05:00–05:00 | 0/0 | not enough data | not measured | not measured | not measured | not measured | not measured |

Own accepted is signed payment. The rest of a headline is not signed payment. This folder does not split that rest into the bot's no-signature hop and outside load.

Flattening (headline rise under half the rise in ours offered) needs the bot's offered rate beside these headlines. It is not computed here.

## Fee tiers

Frozen at 200 and 300 sompi/gram, cap 600, floor 200. A step whose locus quote was above 200 was sat out. Those events are in `gates.csv`.

## Mining share

Locus blocks in the 10-minute rows: 265990 total, 103864 paying this side's miner, 39.05%.

## Gate events

- 2026-10-09T16:57:13.161Z · clock-start
- 2026-10-09T16:58:39.542Z · clock-start
- 2026-10-09T17:24:29.935Z · clock-start
- 2026-10-09T20:15:00.457Z · miner-want
- 2026-10-09T20:15:00.543Z · rehearsal-read
- 2026-10-09T20:30:00.403Z · miner-want
- 2026-10-09T20:30:00.417Z · rehearsal · go · lag 1
- 2026-10-09T20:53:00.725Z · miner-want
- 2026-10-09T20:53:00.782Z · gate · rehearsal-60
- 2026-10-09T20:53:00.964Z · coins-split
- 2026-10-09T20:53:00.972Z · arm
- 2026-10-09T20:53:00.979Z · arm
- 2026-10-09T20:53:00.991Z · arm
- 2026-10-09T20:53:01.017Z · arm
- 2026-10-09T20:53:01.042Z · arm
- 2026-10-09T20:59:03.115Z · step-done · rehearsal-60 · ended
- 2026-10-09T20:59:03.528Z · miner-want
- 2026-10-09T21:00:00.432Z · miner-want
- 2026-10-09T21:10:00.108Z · baseline-B
- 2026-10-09T21:10:00.501Z · miner-want
- 2026-10-09T21:20:00.352Z · miner-want
- 2026-10-09T21:20:00.373Z · gate · C2
- 2026-10-09T21:20:00.408Z · coins-split
- 2026-10-09T21:20:00.413Z · arm
- 2026-10-09T21:20:00.417Z · arm
- 2026-10-09T21:20:00.422Z · arm
- 2026-10-09T21:20:00.428Z · arm
- 2026-10-09T21:20:00.437Z · arm
- 2026-10-09T21:30:03.445Z · step-done · C2 · ended
- 2026-10-09T21:30:03.834Z · miner-want
- 2026-10-09T21:30:03.841Z · gate · C3
- 2026-10-09T21:30:04.073Z · coins-split
- 2026-10-09T21:30:04.078Z · arm
- 2026-10-09T21:30:04.083Z · arm
- 2026-10-09T21:30:04.088Z · arm
- 2026-10-09T21:30:04.093Z · arm
- 2026-10-09T21:30:04.101Z · arm
- 2026-10-09T21:30:52.582Z · clock-start
- 2026-10-09T21:32:49.876Z · clock-start
- 2026-10-09T21:35:33.511Z · clock-start
- 2026-10-09T21:35:33.520Z · baseline-restored
- 2026-10-09T21:35:37.479Z · clock-start
- 2026-10-09T21:35:37.481Z · baseline-restored
- 2026-10-09T21:37:11.072Z · clock-start
- 2026-10-09T21:37:11.074Z · baseline-restored
- 2026-10-09T21:38:13.975Z · clock-start
- 2026-10-09T21:38:13.977Z · baseline-restored
- 2026-10-09T21:44:46.932Z · clock-start
- 2026-10-09T21:44:46.934Z · baseline-restored
- 2026-10-09T21:44:46.935Z · skip-past · stop-and-health
- 2026-10-09T21:44:46.935Z · skip-past · rehearsal-miners
- 2026-10-09T21:44:46.935Z · skip-past · rehearsal-60
- 2026-10-09T21:44:46.935Z · skip-past · rehearsal-wrap
- 2026-10-09T21:44:46.935Z · skip-past · B0
- 2026-10-09T21:44:46.936Z · skip-past · C1
- 2026-10-09T21:44:46.936Z · skip-past · C2
- 2026-10-09T21:44:46.936Z · skip-past · C3
- 2026-10-09T21:44:47.249Z · miner-want
- 2026-10-09T21:44:47.250Z · target · 2x · build 7
- 2026-10-09T21:44:47.270Z · gate · 2x
- 2026-10-09T21:46:17.394Z · coins-refresh
- 2026-10-09T21:46:17.446Z · coins-split
- 2026-10-09T21:46:17.451Z · arm
- 2026-10-09T21:46:17.456Z · arm
- 2026-10-09T21:46:17.460Z · arm
- 2026-10-09T21:46:17.466Z · arm
- 2026-10-09T21:48:07.957Z · clock-start
- 2026-10-09T21:48:08.318Z · miner-want
- 2026-10-09T21:48:08.344Z · rehearsal-read
- 2026-10-09T21:52:09.048Z · clock-start
- 2026-10-09T21:52:09.050Z · baseline-restored
- 2026-10-09T21:52:09.050Z · skip-past · stop-and-health
- 2026-10-09T21:52:09.050Z · skip-past · rehearsal-miners
- 2026-10-09T21:52:09.050Z · skip-past · rehearsal-60
- 2026-10-09T21:52:09.051Z · skip-past · rehearsal-wrap
- 2026-10-09T21:52:09.051Z · skip-past · B0
- 2026-10-09T21:52:09.051Z · skip-past · C1
- 2026-10-09T21:52:09.051Z · skip-past · C2
- 2026-10-09T21:52:09.051Z · skip-past · C3
- 2026-10-09T21:52:09.428Z · miner-want
- 2026-10-09T21:52:09.428Z · target · 2x · build 7
- 2026-10-09T21:52:09.448Z · gate · 2x
- 2026-10-09T21:53:39.601Z · coins-refresh
- 2026-10-09T21:53:39.667Z · coins-split
- 2026-10-09T21:53:39.673Z · arm
- 2026-10-09T21:53:39.678Z · arm
- 2026-10-09T21:53:39.683Z · arm
- 2026-10-09T21:53:39.689Z · arm
- 2026-10-09T21:55:06.345Z · step-done · 2x · ended
- 2026-10-09T22:00:00.378Z · miner-want
- 2026-10-09T22:05:00.334Z · miner-want
- 2026-10-09T22:05:00.335Z · target · 2x-miners-off · build 7
- 2026-10-09T22:05:00.341Z · gate · 2x-miners-off
- 2026-10-09T22:06:30.481Z · coins-refresh
- 2026-10-09T22:06:30.529Z · coins-split
- 2026-10-09T22:06:30.533Z · arm
- 2026-10-09T22:06:30.538Z · arm
- 2026-10-09T22:06:30.542Z · arm
- 2026-10-09T22:06:30.549Z · arm
- 2026-10-09T22:20:03.496Z · step-done · 2x-miners-off · ended
- 2026-10-09T22:25:00.392Z · miner-want
- 2026-10-09T22:30:00.400Z · miner-want
- 2026-10-09T22:30:00.401Z · target · 5x · build 148
- 2026-10-09T22:30:00.412Z · gate · 5x
- 2026-10-09T22:31:30.561Z · coins-refresh
- 2026-10-09T22:31:30.598Z · coins-split
- 2026-10-09T22:31:30.604Z · arm
- 2026-10-09T22:31:30.609Z · arm
- 2026-10-09T22:31:30.614Z · arm
- 2026-10-09T22:31:30.645Z · arm
- 2026-10-09T22:31:30.652Z · arm
- 2026-10-09T22:45:03.435Z · step-done · 5x · ended
- 2026-10-09T22:50:00.336Z · miner-want
- 2026-10-09T22:50:00.337Z · target · 10x · build 363
- 2026-10-09T22:50:00.343Z · gate · 10x
- 2026-10-09T22:51:30.482Z · coins-refresh
- 2026-10-09T22:51:30.509Z · coins-split
- 2026-10-09T22:51:30.514Z · arm
- 2026-10-09T22:51:30.518Z · arm
- 2026-10-09T22:51:30.523Z · arm
- 2026-10-09T22:51:30.529Z · arm
- 2026-10-09T22:51:30.535Z · arm
- 2026-10-09T23:05:04.115Z · step-done · 10x · ended
- 2026-10-09T23:10:00.356Z · miner-want
- 2026-10-09T23:10:00.356Z · target · 20x · build 793
- 2026-10-09T23:10:00.361Z · gate · 20x
- 2026-10-09T23:11:30.491Z · coins-refresh
- 2026-10-09T23:11:30.513Z · coins-split
- 2026-10-09T23:11:30.519Z · arm
- 2026-10-09T23:11:30.523Z · arm
- 2026-10-09T23:11:30.528Z · arm
- 2026-10-09T23:11:30.533Z · arm
- 2026-10-09T23:11:30.538Z · arm
- 2026-10-09T23:25:03.627Z · step-done · 20x · ended
- 2026-10-09T23:30:00.316Z · miner-want
- 2026-10-09T23:30:00.316Z · target · 30x · build 983
- 2026-10-09T23:30:00.322Z · gate · 30x
- 2026-10-09T23:31:30.447Z · coins-refresh
- 2026-10-09T23:31:30.473Z · coins-split
- 2026-10-09T23:31:30.477Z · arm
- 2026-10-09T23:31:30.482Z · arm
- 2026-10-09T23:31:30.487Z · arm
- 2026-10-09T23:31:30.492Z · arm
- 2026-10-09T23:31:30.498Z · arm
- 2026-10-09T23:45:04.365Z · step-done · 30x · ended
- 2026-10-09T23:50:00.342Z · miner-want
- 2026-10-09T23:50:00.343Z · step-done · max · no-seconds
- 2026-10-10T00:15:00.379Z · miner-want
- 2026-10-10T00:25:00.434Z · miner-want
- 2026-10-10T00:25:00.435Z · target · hold · build 983
- 2026-10-10T00:25:00.442Z · gate · hold
- 2026-10-10T00:26:30.615Z · coins-refresh
- 2026-10-10T00:26:30.639Z · coins-split
- 2026-10-10T00:26:30.645Z · arm
- 2026-10-10T00:26:30.650Z · arm
- 2026-10-10T00:26:30.654Z · arm
- 2026-10-10T00:26:30.659Z · arm
- 2026-10-10T00:26:30.664Z · arm
- 2026-10-10T04:45:02.343Z · step-done · hold · ended
- 2026-10-10T04:45:02.652Z · miner-want
- 2026-10-10T05:00:00.012Z · skip-past · end
- 2026-10-10T05:00:00.014Z · miner-want
- 2026-10-10T05:00:01.521Z · clock-end
- 2026-10-10T05:02:18.846Z · clock-start
- 2026-10-10T05:02:18.848Z · baseline-restored
- 2026-10-10T05:02:18.849Z · skip-past · stop-and-health
- 2026-10-10T05:02:18.849Z · skip-past · rehearsal-miners
- 2026-10-10T05:02:18.849Z · skip-past · rehearsal-60
- 2026-10-10T05:02:18.849Z · skip-past · rehearsal-wrap
- 2026-10-10T05:02:18.849Z · skip-past · B0
- 2026-10-10T05:02:18.849Z · skip-past · C1
- 2026-10-10T05:02:18.849Z · skip-past · C2
- 2026-10-10T05:02:18.850Z · skip-past · C3
- 2026-10-10T05:02:18.850Z · skip-past · 2x
- 2026-10-10T05:02:18.850Z · skip-past · settle-off
- 2026-10-10T05:02:18.850Z · skip-past · 2x-miners-off
- 2026-10-10T05:02:18.850Z · skip-past · settle-on
- 2026-10-10T05:02:18.850Z · skip-past · 5x
- 2026-10-10T05:02:18.851Z · skip-past · 10x
- 2026-10-10T05:02:18.851Z · skip-past · 20x
- 2026-10-10T05:02:18.851Z · skip-past · 30x
- 2026-10-10T05:02:18.851Z · skip-past · max
- 2026-10-10T05:02:18.851Z · skip-past · B1
- 2026-10-10T05:02:19.186Z · miner-want
- 2026-10-10T05:02:19.186Z · target · hold · build 983
- 2026-10-10T05:02:19.199Z · gate · hold
- 2026-10-10T05:02:19.476Z · step-done · hold · down

## Labels

**Claim (measured on TN10):** the numbers in the CSV files are what locus and this desk recorded. Build rates are signed payment, mass about 1,624.

**Not sure / open for debate:** whether the outside load in B0 was other people's traffic. Probe and stream ids were not removed from the per-second baseline the clock used for its rate rule.

**Needs more testing:** whether one miner per side lowers the duplicate share. Compare the one-side rows with the ramp in the step table. A gap that is not obvious stays needs more testing.

