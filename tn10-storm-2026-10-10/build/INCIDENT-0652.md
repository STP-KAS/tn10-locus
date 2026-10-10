> **Experimental. We are just trying this.** [Disclaimer](../../../DISCLAIMER.md)

# Locus abort at 06:52Z, Saturday 10 Oct 2026

**Claim (measured on TN10):** locus kaspad aborted at 06:52:56Z, during the rehearsal wait, before Build's 06:53Z send. Windows recorded a fast-fail inside kaspad.exe, exception `0xc0000409`. The process log ends on ordinary accepted blocks. The same abort class happened at 01:28Z during Friday's hold.

**What Build did:** the rehearsal send retried and did not submit while the node was down. One locus process was started again at 06:56Z on the same flags. By 06:57Z it was accepting blocks, synced, sink lag 1 s, and the rehearsal gate passed. Coin refresh then armed 5 senders at 06:58:30Z. The row closed at 06:59:02Z: target 60, mean submit 58, 100% of target, 30 seconds, clean. A desk watcher now starts locus again if that process is gone, with a five-minute wait if it dies within two minutes of a start.

**Not sure / open for debate:** the cause of `0xc0000409` inside this kaspad build. It is not a sender crash. No sender was armed at 06:52Z.

Counts only. No txid, key, seed, host, IP, port or address.
