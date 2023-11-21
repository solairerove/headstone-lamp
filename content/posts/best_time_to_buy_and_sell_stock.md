---
title: 121. Best Time to Buy and Sell Stock
description: find the maximum difference between two numbers in the array
date: 2023-11-21
tags: [ dp, array, easy ]
---

```python
# O(n) time || O(1) space
def max_profit(self, prices: List[int]) -> int:
    min_price, res = prices[0], 0
    for price in prices[1:]:
        if price < min_price:
            min_price = price
        else:
            res = max(res, price - min_price)

    return res
```

The idea is to find the maximum difference between two numbers in the array where the smaller number comes before the
larger number. This difference represents the maximum profit.
