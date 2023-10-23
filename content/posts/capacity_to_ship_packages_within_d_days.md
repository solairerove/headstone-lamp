---
title: 1011. Capacity To Ship Packages Within D Days
description: the low is max weight, the high is sum of weights, use bs
date: 2023-10-23
tags: [ binary-search, medium ] 
---

```python
# O(n * log(n)) time || O(1) space
def ship_within_days(self, weights: List[int], days: int) -> int:
    low, high = max(weights), sum(weights)
    while low <= high:
        mid = low + (high - low) // 2
        days_required, curr_weight = 1, 0

        for weight in weights:
            if curr_weight + weight <= mid:
                curr_weight += weight
            else:
                days_required, curr_weight = days_required + 1, weight

        if days_required <= days:
            high = mid - 1
        else:
            low = mid + 1

    return low
```


Determine the search space: \
The minimum possible weight capacity of the ship would be the maximum weight among all the packages, \
and the maximum possible weight capacity of the ship would be the sum of all the package weights.

Use binary search: \
Set the lower bound of the binary search as the maximum package weight \
and the upper bound as the sum of all the package weights.

While the lower bound is less than or equal to the upper bound, perform the following steps:

    a. Calculate the mid weight capacity of the ship by taking the average of the lower and upper bounds: 
        mid = (lower_bound + upper_bound) // 2

    b. Simulate the shipment process: 
        Create variables to track the number of days and the current weight being shipped. 
        Iterate through the list of weights and for each weight: 

        If the current weight + weight of the package is less than or equal to the mid capacity, 
        add the package to the current shipment weight.
        If the current weight + weight of the package exceeds the mid capacity, 
        increment the number of days and reset the current shipment weight to the weight of the current package. 

    c. Compare the number of days with the given days parameter. 

        If the number of days is less than or equal to the given days, 
        it means the weight capacity is sufficient. So, update the upper bound to mid - 1. 
        If the number of days is greater than the given days, 
        it means the weight capacity is not sufficient. So, update the lower bound to mid + 1.

Return the least weight capacity: \
Once the binary search is complete (lower_bound > upper_bound), \
return the lower bound value as the least weight capacity that will result in all packages being shipped within days.
