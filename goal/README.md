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

A synced node can show more transaction slots inside blocks than the virtual chain accepts. On 9 Oct the extras were duplicates, not lost transactions.

- **Claim (measured on TN10):** on keel, 9 Oct 2026, 48–49% of tx slots in blocks were copies of a transaction already in another block of the same minute (12:29 and 12:55 UTC). In 3 of the 4 valid windows, 97–100% of distinct transactions were accepted, and every transaction seen only in a red block was accepted too. Transactions in blocks off the selected chain still count when a chain block merges them. Source: [tn10-monitoring-plan-2026-10-09](../tn10-monitoring-plan-2026-10-09/README.md), commit `94929a9`.
- **Not sure / open for debate:** parallel blocks built from overlapping mempools pick the same transactions. The duplicate share was about 48% when our miners made 35% of the blocks, and 13–15% when they made 2–4%.
- **Needs more testing:** whether one miner per side, mining where that side sends, lowers the duplicate share. Tonight's one-side control measures it.

Extra hash does not add blocks. The difficulty adjustment spends it to hold about 10 blocks a second.

A fee above the competing transactions takes slots inside a full block. It does not make the block larger. Submit faster than the mass you actually win, and the mempool fills. The chain rate does not move.

## What to do

For a signed payment, the reachable line is about 3,080 accepted tx/s:

1. Raise distinct transactions per block, not submits. Fewer copies of the same transaction across parallel blocks is the room left under about 3,080.
2. Each side mines where it sends, one miner per node. Cutting miners is not tonight's change. **Needs more testing.**
3. No filler aimed at 3,100 tx/s. The steps find where acceptance flattens.
4. Keep the fee pair 200 and 300 unless the normal quote is above 200. A higher fee reorders inside full blocks. It does not add room.
5. Keep the hop at one input, one output, no change.

To go past that line, and to make 3,500 fit, use the 643-mass hop. Its outputs are anyone-can-spend: label every number from it **anyone-can-spend hops, not realistic payments**. Do not send more than a full block can accept.

## How to read it

Count for one minute on a synced node.

- Unique accepted transaction ids from the virtual-chain notification. That is the rate.
- Blocks added, and the transactions carried in those blocks.
- Selected-chain blocks in the same minute.
- Duplicate share: 1 − unique ids in blocks / tx slots in blocks.

Write the minute in UTC. A blank minute is not measured. Hosts, addresses, and transaction ids stay out of this repo.

---

Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
