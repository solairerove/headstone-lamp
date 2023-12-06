---
title: 309. Best Time to Buy and Sell Stock with Cooldown
description: buy, sell, cooldown
date: 2023-11-22
tags: [ dp, arrays, medium ]
---

```python
# O(n) time || O(1) space
def max_profit(self, prices: List[int]) -> int:
    buy, sell, cooldown = -prices[0], 0, 0
    for price in prices[1:]:
        _buy = max(buy, cooldown - price)
        _sell = buy + price
        _cooldown = max(cooldown, sell)

        buy, sell, cooldown = _buy, _sell, _cooldown

    return max(sell, cooldown)
```

For this LeetCode problem, the challenge is to find the maximum profit from buying and selling stocks with a constraint:
after selling a stock, you must have a cooldown period of one day before you can buy again. To solve this problem, we
can use dynamic programming, where we maintain three states at each day:

1) Buy: The maximum profit on day `i` if we buy the stock on this day. This state can only be reached from the cooldown
   state of the previous day.
2) Sell: The maximum profit on day `i` if we sell the stock on this day. This state can be reached from the buy state of
   the previous day.
3) Cooldown: The maximum profit on day `i` if we are in the cooldown state on this day. This state can be reached either
   from the sell state or the cooldown state of the previous day.

Here's how you can implement the solution:

1) Initialize Variables:
    - `buy`: Initially set to `-prices[0]` because we spend `prices[0]` money to buy the stock.
    - `sell`: Initially set to 0, as we haven't made any profit yet.
    - `cooldown`: Initially set to 0, as we haven't sold any stock yet.

2) Iterate Through the Array:
    - For each day, calculate the new values of `buy`, `sell`, and `cooldown`:
        - `new_buy` is the maximum of the previous `buy` and the `cooldown` from the previous day minus today's price (
          since buying costs money).
        - `new_sell` is the maximum of the previous `sell` and the `buy` from the previous day plus today's price (since
          selling earns money).
        - `new_cooldown` is the maximum of the previous `cooldown` and the `sell` from the previous day.
    - Update `buy`, `sell`, and `cooldown` with these new values for the next iteration.

3) Return the Maximum of `sell` and `cooldown`:
    - At the end, the maximum profit will be the maximum of the `sell` and `cooldown` states, as you can't end with a
      buy.

```python
# O(n) time || O(n) space
def max_profit_top_down(self, prices: List[int]) -> int:
    @lru_cache(None)
    def dp(i, holding):
        if i >= len(prices):
            return 0

        if holding:
            res = max(prices[i] + dp(i + 2, False), dp(i + 1, True))
        else:
            res = max(-prices[i] + dp(i + 1, True), dp(i + 1, False))

        return res

    return dp(0, False)
```
