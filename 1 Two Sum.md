# 1. Two Sum

Difficulty: easy
Link: https://leetcode.com/problems/two-sum
Topic: Array

### Problem Analysis

The task is to find two distinct indices in the array such that the numbers at those indices sum up to the target value. The function should return these two indices.

**Examples**:

- Input: `nums = [2, 7, 11, 15]`, `target = 9`
    - Output: `[0, 1]`
    - Explanation: The numbers at indices `0` and `1` (2 + 7) sum to 9.
- Input: `nums = [3, 2, 4]`, `target = 6`
    - Output: `[1, 2]`
    - Explanation: The numbers at indices `1` and `2` (2 + 4) sum to 6.
- Input: `nums = [3, 3]`, `target = 6`
    - Output: `[0, 1]`
    - Explanation: The numbers at indices `0` and `1` (3 + 3) sum to 6.

### Approach

1. **Brute Force**: The simplest approach is to check every possible pair of numbers in the array to see if their sum equals the target. However, this approach is not efficient for large arrays.
    - **Time Complexity**: O(n²)
    - **Space Complexity**: O(1)
2. **Hash Map (Optimal Solution)**: We can use a hash map (dictionary) to store the numbers we’ve seen so far and their corresponding indices. For each number, we check if the complement (i.e., `target - num`) exists in the hash map. If it does, we return the indices.
    - **Time Complexity**: O(n), where n is the length of the array. Each element is processed once.
    - **Space Complexity**: O(n), due to the additional space needed to store elements in the hash map.

### Decision

Given the problem constraints and the need for efficiency, the **Hash Map Approach** is the best solution. It allows us to find the two indices in a single pass through the array.

### Code Implementation

```python
def two_sum(nums, target):
    # Step 1: Create a hash map to store numbers and their indices
    num_to_index = {}

    # Step 2: Iterate through the array
    for i, num in enumerate(nums):
        # Step 3: Calculate the complement that would sum to the target
        complement = target - num

        # Step 4: Check if the complement is already in the hash map
        if complement in num_to_index:
            return [num_to_index[complement], i]  # return the indices

        # Step 5: Add the current number and its index to the hash map
        num_to_index[num] = i

    # Step 6: If no solution is found (though the problem guarantees one), return an empty list
    return []

```

### Edge Cases

1. **Multiple Solutions**: The problem guarantees exactly one solution, so we don’t need to handle multiple valid pairs.
2. **All Elements the Same**: Arrays where all elements are the same should still function correctly if the target is twice any element.
3. **No Valid Pairs**: Although the problem states there is exactly one solution, in a more general scenario, we could return an empty list if no valid pairs exist.

### Unit Test

```python
import unittest

class TestTwoSum(unittest.TestCase):

    def test_basic(self):
        self.assertEqual(two_sum([2, 7, 11, 15], 9), [0, 1])

    def test_with_duplicates(self):
        self.assertEqual(two_sum([3, 2, 4], 6), [1, 2])

    def test_all_same_elements(self):
        self.assertEqual(two_sum([3, 3], 6), [0, 1])

    def test_no_solution(self):
        self.assertEqual(two_sum([1, 2, 3], 7), [])

    def test_large_numbers(self):
        self.assertEqual(two_sum([1000000, 500000, 500000], 1000000), [1, 2])

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

### Alternative Approach

**Brute Force**: Although it's less efficient, it's sometimes useful to compare simpler methods for smaller inputs or learning purposes.

```python
def two_sum_brute_force(nums, target):
    # Step 1: Iterate through each pair of numbers
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            # Step 2: Check if the current pair sums to the target
            if nums[i] + nums[j] == target:
                return [i, j]

    # Step 3: If no solution is found (shouldn't happen in this problem), return an empty list
    return []
```

This approach is straightforward but has a time complexity of O(n²), making it inefficient for larger arrays. The hash map solution is preferred due to its optimal performance.