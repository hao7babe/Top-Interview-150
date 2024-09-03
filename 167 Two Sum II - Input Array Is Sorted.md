# 167. Two Sum II - Input Array Is Sorted

Difficulty: Medium
Link: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted
Topic: Array

### Problem Analysis

The problem requires finding two indices in a sorted array such that the sum of the elements at these indices equals a given target. Since the array is sorted, we can take advantage of this property to find a more efficient solution.

**Examples**:

- Input: `numbers = [2,7,11,15]`, `target = 9`
    - Output: `[1, 2]`
- Input: `numbers = [2,3,4]`, `target = 6`
    - Output: `[1, 3]`

### Approach

1. **Two-Pointer Approach**: The most efficient way to solve this problem is to use two pointers. One pointer starts at the beginning of the array, and the other starts at the end. We check the sum of the elements at these pointers:
    - If the sum equals the target, we return the current indices.
    - If the sum is less than the target, we move the left pointer to the right to increase the sum.
    - If the sum is greater than the target, we move the right pointer to the left to decrease the sum.
2. **Brute Force Approach**: A less efficient approach is to check every possible pair of elements to see if they sum to the target. This would have a time complexity of O(n²), which is not ideal for large arrays.

### Time and Space Complexity

- **Two-Pointer Approach**:
    - **Time Complexity**: O(n), where n is the length of the array. Each element is processed at most once.
    - **Space Complexity**: O(1), as no additional data structures are needed.
- **Brute Force Approach**:
    - **Time Complexity**: O(n²), since every pair of elements is checked.
    - **Space Complexity**: O(1), as it only requires a few variables for the indices and sums.

Given the problem's constraints and the fact that the array is sorted, the **Two-Pointer Approach** is clearly the best choice in terms of efficiency.

### Code Implementation

```python
def two_sum(numbers, target):
    # Step 1: Initialize two pointers, left at the start and right at the end of the array
    left, right = 0, len(numbers) - 1

    # Step 2: Loop until the pointers cross each other
    while left < right:
        # Step 3: Calculate the current sum of the elements at the two pointers
        current_sum = numbers[left] + numbers[right]

        # Step 4: Check if the current sum matches the target
        if current_sum == target:
            return [left + 1, right + 1]  # return 1-based indices
        elif current_sum < target:
            left += 1  # move the left pointer to the right
        else:
            right -= 1  # move the right pointer to the left

    # Step 5: If no solution is found (which shouldn't happen in this problem), return an empty list
    return []

```

### Edge Cases

1. **Minimum Length Array**: If the array has only two elements, the function should return `[1, 2]`.
2. **All Elements are the Same**: If all elements are the same and their sum equals the target, it should return the first and last indices.
3. **No Valid Pairs**: Although the problem guarantees a solution, in a different context, this edge case could return an empty list.

### Unit Test

```python
import unittest

class TestTwoSum(unittest.TestCase):

    def test_basic(self):
        self.assertEqual(two_sum([2, 7, 11, 15], 9), [1, 2])

    def test_small_array(self):
        self.assertEqual(two_sum([2, 3, 4], 6), [1, 3])

    def test_negative_numbers(self):
        self.assertEqual(two_sum([-1, 0], -1), [1, 2])

    def test_large_numbers(self):
        self.assertEqual(two_sum([1, 3, 5, 7, 10, 11, 15], 18), [4, 7])

    def test_same_elements(self):
        self.assertEqual(two_sum([2, 2, 2, 2], 4), [1, 2])

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

### Alternative Approach

```python
def two_sum_brute_force(numbers, target):
    # Step 1: Iterate through each pair of numbers
    for i in range(len(numbers)):
        for j in range(i + 1, len(numbers)):
            # Step 2: Check if the current pair sums to the target
            if numbers[i] + numbers[j] == target:
                return [i + 1, j + 1]  # return 1-based indices
    # Step 3: If no solution is found, return an empty list (shouldn't happen in this problem)
    return []
```