---
title: 122. Best Time to Buy and Sell Stock II
description: whenever `prices[i]` is greater than `prices[i - 1]`, we can consider it as a profit-making
date: 2023-11-21
tags: [ dp, arrays, medium ]
---

```python
# O(n) time || O(1) space
def max_profit(self, prices: List[int]) -> int:
    res = 0
    for i in range(1, len(prices)):
        if prices[i] > prices[i - 1]:
            res += prices[i] - prices[i - 1]

    return res
```

```python
# O(n) time || O(1) space
def max_profit_lambda(self, prices: List[int]) -> int:
    return reduce(lambda profit, i: profit + max(prices[i] - prices[i - 1], 0), range(1, len(prices)), 0)
```

This LeetCode problem asks for the maximum profit that can be achieved by buying and selling stocks, with the
possibility of conducting multiple transactions. However, you can't engage in multiple transactions at once (i.e., you
must sell the stock before you buy again).

The key insight for this problem is that we can accumulate profit from every increase in price from one day to the next.
In other words, whenever `prices[i]` is greater than `prices[i - 1]`, we can consider it as a profit-making opportunity
and add this difference to our total profit.

Here's how you can approach this problem:

1) Initialize a Variable for Total Profit:
    - Set `total_profit` to 0. This will accumulate the total profit from all transactions.
2) Iterate Through the Array:
    - Start iterating from the second element of the array.
    - If the current price is greater than the previous day's price, it means buying on the previous day and selling
      today would result in a profit. Add this profit to total_profit.
3) Return `total_profit`:
    - After iterating through the array, `total_profit` will contain the maximum profit that can be achieved with the
      given stock prices.
