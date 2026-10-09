> **Experimental. We are just trying this.**
>
> [Disclaimer](../DISCLAIMER.md)

# Included rate over 3,000 tx/s

This page is a recommendation. It does not start the storm, it does not move T0, and it does not change the fee pair in the questions plan. Clocks on this page are UTC.

The score is transactions the virtual chain accepts per second. Transactions offered, and transactions written into a block that the virtual chain does not accept, are different numbers. Locus and keel are two views of one chain. Add each side's own accepted transactions. Do not add the same accepted id twice.

## The block

rusty-kaspa v2.1.0 gives each block three mass budgets: compute 500,000, storage 500,000, transient 1,000,000. The live network aims at about 10 blocks a second. That rate is the difficulty adjustment. It is not a flag on the node.

A signed one-input, one-output payment is about 1,624 compute mass. 500,000 / 1,624 is about 308 of those payments in one block. At 10 blocks a second the same shape is about 3,080 tx/s. A block that already holds about 308 of them is full. Another runner, another miner, another socket, or a higher fee does not add mass to that block.

3,500 of those signed payments need about 568,000 compute mass in one block. They do not fit. The 7 Oct tries did not read 3,500 for this shape.

A lighter hop does fit. A one-input, one-output hop with no signature measured 643 mass. 500,000 / 643 is about 778 per block, about 7,780 tx/s at 10 blocks a second. 3,500 of those need about 225,000 mass, which fits. The outputs of that hop are anyone-can-spend. On this testnet the coins are the test float, and each lane stays small so a stranger cannot empty the wallet. Storage mass stays near zero when the output amount is close to the input amount. A fat change output, or a fan-out into tiny outputs, hits the storage budget and the rate falls.

## Why two runners stay under the cap

Both runners write into the same 500,000 mass. Once blocks are full, the second runner takes slots from the first. It does not open a second budget.

A synced node can show more transactions inside blocks than the virtual chain accepts. Those extras sit in blocks that are not merged. Extra miners raise the chance of finding a block, and the difficulty adjustment spends that hash to hold about 10 blocks a second. Hash above that line makes more blocks that miss the selected chain. Transactions in those blocks do not raise the accepted rate.

A fee above the competing transactions takes slots inside a full block. It does not make the block larger. Submit faster than the mass you actually win, and the mempool fills. The chain rate does not move.

## What to do

For a signed payment, the reachable line is about 3,080 accepted tx/s:

1. One filler near 3,100 tx/s. The other runner only fills mass the first one leaves empty.
2. Enough miners to hold about 10 blocks a second, and no more. Most blocks should be blue.
3. Pay the live normal quote, so the filler's transactions are the ones in the block.
4. Keep the hop at one input, one output, no change.

To go past that line, and to make 3,500 fit, use the 643-mass hop. Keep the same rule on miners and on submit: do not send more than a full block can accept.

## How to read it

Count for one minute on a synced node.

- Unique accepted transaction ids from the virtual-chain notification. That is the rate.
- Blocks added, and the transactions carried in those blocks.
- Selected-chain blocks in the same minute.

Write the minute in UTC. A blank minute is not measured. Hosts, addresses, and transaction ids stay out of this repo.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
