---
title: 121. Best Time to Buy and Sell Stock
description: find the maximum difference between two numbers in the array
date: 2023-11-21
tags: [ dp, arrays, easy ]
---

```python
# O(n) time || O(1) space
def max_profit(self, prices: List[int]) -> int:
    min_price, max_profit = prices[0], 0
    for i in range(1, len(prices)):
        min_price = min(min_price, prices[i])
        max_profit = max(max_profit, prices[i] - min_price)

    return max_profit
```

```python
# O(n) time || O(1) space
def max_profit_lambda(self, prices: List[int]) -> int:
    return reduce(lambda acc, price: (min(acc[0], price), max(acc[1], price - acc[0])), prices[1:], (prices[0], 0))[1]
```

The idea is to find the maximum difference between two numbers in the array where the smaller number comes before the
larger number. This difference represents the maximum profit.
