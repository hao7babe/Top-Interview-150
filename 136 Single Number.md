# 136. Single Number

Difficulty: easy
Link: https://leetcode.com/problems/single-number
Topic: Array

### Problem Analysis

The problem asks us to find the single element in an array where every other element appears exactly twice. In other words, given an array of integers where every element appears twice except for one, we need to find that unique element.

**Examples**:

- Input: `nums = [2, 2, 1]`
    - Output: `1`
- Input: `nums = [4, 1, 2, 1, 2]`
    - Output: `4`
- Input: `nums = [1]`
    - Output: `1`

### Approach

1. **Using XOR** (Optimal Approach):
    - XOR has a few useful properties that we can leverage:
        - `a ^ a = 0`: XOR-ing a number with itself results in 0.
        - `a ^ 0 = a`: XOR-ing a number with 0 results in the number itself.
        - XOR is both commutative and associative, meaning the order of operations doesn't matter.
    - By XOR-ing all the numbers together, pairs of numbers that appear twice will cancel out (i.e., become 0), leaving only the single number.
2. **Hash Map** (Alternative Approach):
    - Use a hash map (or dictionary) to count the frequency of each number. The number that appears only once is the result.

### Time and Space Complexity

- **XOR Approach**:
    - **Time Complexity**: O(n), where n is the length of the array. We traverse the array once.
    - **Space Complexity**: O(1), since no additional data structures are needed.
- **Hash Map Approach**:
    - **Time Complexity**: O(n), since we iterate through the array and use a hash map to count the occurrences.
    - **Space Complexity**: O(n), since we need additional space to store the count of each number.

Given these considerations, the **XOR Approach** is both time and space efficient.

### Edge Cases

1. **Single Element**: If the array contains only one element, that element is the answer.
2. **All Elements Paired**: If all other elements appear exactly twice, XOR-ing will cancel them out, leaving only the unique element.

### Code Implementation (XOR Approach)

```python
def single_number(nums):
    # Step 1: Initialize a variable to store the XOR result
    result = 0

    # Step 2: XOR all numbers in the array
    for num in nums:
        result ^= num  # XOR accumulates the result

    # Step 3: Return the single number
    return result

```

### Unit Test

```python
import unittest

class TestSingleNumber(unittest.TestCase):

    def test_single_number_basic(self):
        self.assertEqual(single_number([2, 2, 1]), 1)

    def test_larger_array(self):
        self.assertEqual(single_number([4, 1, 2, 1, 2]), 4)

    def test_single_element(self):
        self.assertEqual(single_number([1]), 1)

    def test_negative_numbers(self):
        self.assertEqual(single_number([1, -1, 2, -1, 2]), 1)

    def test_large_numbers(self):
        self.assertEqual(single_number([9999999, 9999999, 123456789]), 123456789)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Alternative Approach (Hash Map)

```python
def single_number(nums):
    # Step 1: Create a dictionary to count occurrences of each number
    count = {}

    # Step 2: Populate the dictionary with frequencies
    for num in nums:
        count[num] = count.get(num, 0) + 1

    # Step 3: Return the number that appears only once
    for num in count:
        if count[num] == 1:
            return num

```

### Summary

- The **XOR Approach** is the most efficient, with O(n) time complexity and O(1) space complexity. This makes it ideal for solving the problem with large arrays.
- The **Hash Map Approach** is straightforward and works well for learning purposes, but it requires extra space.