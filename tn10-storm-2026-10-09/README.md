> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md)

# TN10 storm, Friday 9 Oct 2026: failed run

This night did not execute the plan. The desk report is [build/RUN-REPORT.md](build/RUN-REPORT.md). Keel's desk log for the bot's monitor is [build/desk-keel-log.md](build/desk-keel-log.md) (read 20:45Z). The next run is Saturday 10 Oct, folder [tn10-storm-2026-10-10](../tn10-storm-2026-10-10/README.md). `build/steps-utc.json` in this folder is the voided 21:00Z clock. Commit 3705ee8 put that file back on main at 05:10Z. It is not the Saturday clock.

- `bot/`: the bot's results from keel.
- `build/`: Build's results from locus, including `precheck.md`.
- `COMBINED.md`: written by the bot from both folders. The headline is network unique accepted tx/s counted once from chain data (GO files §12), never locus accepted plus keel accepted. Rates are split signed payment against no-signature hop.

Counts only. No txid, key, seed, host, IP, port or address.
