# 121. Best Time to Buy and Sell Stock

Difficulty: easy
Link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock
Topic: Array

### Problem Analysis

The problem asks us to find the maximum profit that can be achieved by buying and selling a stock given its price on different days. You are allowed to make only one purchase and one sale.

**Examples**:

- Input: `prices = [7, 1, 5, 3, 6, 4]`
    - Output: `5`
    - Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6 - 1 = 5.
- Input: `prices = [7, 6, 4, 3, 1]`
    - Output: `0`
    - Explanation: No profit can be made since the prices only drop.

### Approach

The goal is to maximize the profit by finding the smallest price to buy and the highest price to sell afterward. To achieve this, we can use a single pass through the list while keeping track of the minimum price encountered so far and the maximum profit.

1. **Track Minimum Price**: As we iterate through the prices, we keep track of the lowest price seen so far.
2. **Calculate Profit**: For each price, calculate the potential profit if the stock were sold at that price.
3. **Update Maximum Profit**: Keep track of the maximum profit encountered during the iteration.

### Time and Space Complexity

- **Time Complexity**: O(n), where n is the length of the `prices` array. We only pass through the list once.
- **Space Complexity**: O(1), since we are using a constant amount of extra space.

### Edge Cases

1. **Single-Day Prices**: If there's only one price, no transaction can be made, so the profit should be `0`.
2. **All Decreasing Prices**: If prices only decrease, the best profit is `0` since no profitable transaction can be made.
3. **No Prices**: An empty list should return `0` as there are no prices to make any transaction.

### Code Implementation

```python
def max_profit(prices):
    # Step 1: Initialize variables to track the minimum price and maximum profit
    min_price = float('inf')
    max_profit = 0

    # Step 2: Iterate through the list of prices
    for price in prices:
        # Step 3: Update the minimum price if the current price is lower
        if price < min_price:
            min_price = price
        # Step 4: Calculate the profit if selling at the current price
        elif price - min_price > max_profit:
            max_profit = price - min_price

    # Step 5: Return the maximum profit found
    return max_profit
```

### Unit Test

```python
import unittest

class TestMaxProfit(unittest.TestCase):

    def test_basic_profit(self):
        self.assertEqual(max_profit([7, 1, 5, 3, 6, 4]), 5)

    def test_no_profit(self):
        self.assertEqual(max_profit([7, 6, 4, 3, 1]), 0)

    def test_single_price(self):
        self.assertEqual(max_profit([7]), 0)

    def test_empty_prices(self):
        self.assertEqual(max_profit([]), 0)

    def test_all_same_prices(self):
        self.assertEqual(max_profit([3, 3, 3, 3, 3]), 0)

    def test_profit_at_the_end(self):
        self.assertEqual(max_profit([2, 4, 1, 2, 5, 7]), 6)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

### Summary

- The algorithm efficiently determines the maximum profit by iterating through the prices just once, keeping track of the lowest purchase price and the highest potential profit.
- This approach is optimal with O(n) time complexity and O(1) space complexity.
- Edge cases such as an empty list or all decreasing prices are handled appropriately, ensuring robustness.