# Run report, Friday 9 Oct 2026

**Claim (measured on TN10):** this night did not execute the restart plan. The desk ran the voided 21:00Z clock from 21:52Z and stopped at 05:00Z. It is not a measurement of the plan in the GO files.

The restart that was published set the first gate at 21:45Z, T0 at 22:30Z, and the end at 06:30Z on Saturday 10 Oct. Rates and step order were the same plan. That clock did not stay in force.

## What the desk clock did

From `gates.jsonl` on the desk. Counts only.

| UTC | What happened | Result |
|---|---|---|
| 20:30 | Rehearsal marked go on the voided clock. Keel lag 1 s. | go |
| 20:53–20:59 | Rehearsal send, target 60 tx/s. | not clean. Mean submit 15 tx/s, 100% of that accepted, saturated from second 119. |
| 21:20–21:30 | Build-only row of the voided clock, target 60. | not clean. Mean submit 0. |
| 21:44 and 21:52 | New clock processes skipped the 21:45Z gate, the rehearsal, B0, and the one-side rows. | The step file on the desk was the voided 21:00Z clock again. |
| 21:52–21:55 | 2× on that voided clock. Baseline restored as 67 tx/s, so Build's target was 7. | clean. Mean submit 7. |
| 22:05–22:20 | Miners-off check, target 7. | clean. Mean submit 6.9. |
| 22:30–22:45 | 5×, target 148. | clean. Mean submit 146.4. |
| 22:50–23:05 | 10×, target 363. | clean. Mean submit 359.4. |
| 23:10–23:25 | 20×, target 793. | clean. Mean submit 784.9. |
| 23:30–23:45 | 30×, target 983. | clean. Mean submit 971.5. |
| 23:50 | Max step. | not run. No seconds. |
| 00:25–04:45 | Long hold at 983 tx/s. | not clean. Mean submit 233.2 tx/s, 23.9% accepted, over 15,508 s. |
| 05:00 | Clock ended and asked for the miner off. | The voided end, 90 minutes before the restart end. |
| 05:02 | A new process tried to resume the hold. | Armed 0. Locus RPC was down. The row was closed on that one failure. |

The 67 tx/s baseline was restored from the partial run. There was no fresh B0. The clean early steps are the low-rate path that baseline produces. They are not the storm sized for a baseline near 1,600 tx/s.

## Why it failed

**Claim (measured on TN10):**

- The step file the desk clock reads was overwritten back to the voided 21:00Z clock after the restart file had been put in place. At 21:52Z a second holder started (the scheduled task's last run) and followed that old file.
- More than one holder was started. Clocks exited with code -1.
- Locus kaspad aborted at about 01:28Z. The process error is `fatal runtime error: Rust cannot catch foreign exceptions`. Its log's last line is 01:28Z. The hold clock kept going until 04:45Z with the node gone, which is the low accept rate on the hold.
- The clock treats one failed locus read as the end of the row. At 05:02Z that closed the resumed hold with no senders. It does not retry.
- The logger was set to stop at 05:00Z, so a logger started after that exited at once.
- At 05:10Z the desk publisher committed `3705ee8` and pushed it. That commit replaced the restart step file (T0 22:30Z) with the voided step file (T0 21:00Z). The publisher adds the whole Friday build folder, and the step file lives in that folder.

**Not sure / open for debate:** what wrote the old step file back on the desk between 21:48Z and 21:52Z. The scheduled task starts the holder. It does not write the step file. The file was already the voided clock when that holder started. After 05:10Z, main itself carried that voided file, so a later checkout restores it.

## What the next run changes

Same plan, new clock, Saturday 10 Oct 2026. First gate 06:15Z. T0 07:00Z. End 15:00Z. The desk clock refuses a step file whose T0 is not 07:00Z. It does not restore a baseline from before 06:15Z. A down locus is retried until that row's send window ends. Results for this run go to `tn10-storm-2026-10-10/`, not this folder.

Locus was started again at 05:04Z and was still resyncing its UTXO index when this report was written. The 06:15Z gate is the check. If it is not synced, the rehearsal is not run.
