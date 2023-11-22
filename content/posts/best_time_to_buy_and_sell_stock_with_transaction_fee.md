---
title: 714. Best Time to Buy and Sell Stock with Transaction Fee
description: you only want to complete a transaction when the profit exceeds the transaction fee
date: 2023-11-22
tags: [ dp, array, medium ]
---

```python
# O(n) time || O(1) space
def max_profit(self, prices: List[int], fee: int) -> int:
    res, hold = 0, -prices[0]
    for price in prices[1:]:
        res = max(res, hold + price - fee)
        hold = max(hold, res - price)

    return res
```

A dynamic programming approach can be efficient here. The idea is to keep track of two variables at each step:

1) `Cash`: The maximum profit we can have if we don't hold a stock at the end of day i.
2) `Hold`: The maximum profit we can have if we do hold a stock at the end of day i.

Here's the step-by-step approach:

1) Initialize Variables:
   - `cash` is initially 0 since we start without any stock.
   - `hold` is initially `-prices[0]` since buying a stock would cost us `prices[0]`.

2) Iterate Through the Array:
   - For each day's price, calculate the new `cash` and `hold` values:
     - `new_cash` is the maximum of the previous `cash` and the profit from selling the stock today `(hold + price - fee)`.
     - `new_hold` is the maximum of the previous `hold` and the balance after buying the stock today `(cash - price)`.
   - Update `cash` and `hold` with these new values for the next iteration.

3) Return `cash`:
   - At the end, `cash` will contain the maximum profit that can be achieved.
