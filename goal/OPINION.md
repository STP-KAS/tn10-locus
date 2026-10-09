> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

# Opinion: tx, tx/s, and the 3,000 line

This is an opinion on [goal/README.md](README.md) and on the 9 Oct measurements in [monitoring-result](../monitoring-result/bot-result/README.md). It does not start the storm and it does not move T0.

## tx and tx/s are different counts

A transaction is one id. tx/s is how many ids land in one second. The word TPS only means tx/s. The run produced three counts, and they are not interchangeable.

1. Submitted. What a runner offered the mempool.
2. Slots in blocks. The same id copied into several parallel blocks counts once per copy.
3. Unique accepted. Each id once, when the virtual chain accepts it.

Slots can read about 3,600/s while unique accepted reads about 1,800–2,400/s. That gap is copies, measured at 48–49% of slots in the 12:29 and 12:55 UTC windows. A copy is still a transaction in a block. It is not a second accepted payment.

Adding locus accepted to keel accepted counts the same ids twice. Those nodes see one chain.

## Why 3,000 unique accepted was not reached

A signed one-input, one-output payment is about 1,624 mass. A block holds 500,000 mass, about 308 of those payments. At about 10 blocks/s the mass line is about 3,080 unique tx/s. 3,000 fits in that budget only when almost every slot is a different id.

On 9 Oct the blocks were already full, about 300–350 transactions each. Unique ids inside those blocks stayed about 1,550–2,250/s. Where the miners' share was about 35%, about half the slots were a transaction already present in another block of the same minute. The healthy keel windows averaged 1,627 unique accepted tx/s, with a max of 2,435. Build's own clean stretch on locus was 2,177 accepted tx/s, and its peak minute submitted 2,673. No valid window held 3,000 unique accepted tx/s.

The mass was spent on repeats. Repeats do not raise the unique accepted count. With about half the slots copied, the unique rate sits near half of 3,080, about 1,600. That is the reading of this run.

3,000 unique signed payments is inside the mass budget when the duplicate share is near zero: about 308 different ids in each of about 10 blocks. This run did not produce that share. Whether one miner on each side, mining the transactions that side created, lowers the copies is still open. Four colored windows are not enough, and keel's health changed in the same hours.

3,500 unique signed payments do not fit. 350 of them need about 568,000 mass. The block holds 500,000.

The 643-mass hop can hold 3,000 and 3,500 in the mass budget. It is an anyone-can-spend hop, not a signed payment. The bot's load on 9 Oct already used that shape, and the unique accepted rate was still about 1,600–2,400. The light hop did not produce 3,000 unique accepted tx/s that afternoon. The copies and the keel lag did the limiting.

## What I would count

One number, from one synced node: unique accepted ids per second. Next to it, slots per second and the duplicate share, so a full block of copies is not reported as a higher TPS.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
