# 283. Move Zeroes

Difficulty: easy
Link: https://leetcode.com/problems/move-zeroes
Topic: Array

### Problem Analysis

The problem asks us to move all the zeros in a given array to the end while maintaining the relative order of the non-zero elements. This must be done **in-place** without making a copy of the array.

**Examples**:

- Input: `nums = [0,1,0,3,12]`
    - Output: `[1,3,12,0,0]`
- Input: `nums = [0,0,1]`
    - Output: `[1,0,0]`

### Approach

1. **Two-Pointer Approach**:
    - Use two pointers: one (`left`) to track the position where the next non-zero element should go and another (`right`) to iterate through the array.
    - As you iterate, when you find a non-zero element, swap it with the element at the `left` pointer's position and increment `left`.
    - This approach ensures that all non-zero elements are moved to the front, and zeros are shifted to the end.

### Time and Space Complexity

- **Time Complexity**: O(n), where n is the length of the array. We pass through the array only once.
- **Space Complexity**: O(1), since we are modifying the array in place and not using extra space.

### Code Implementation

```python
def move_zeroes(nums):
    # Step 1: Initialize the left pointer
    left = 0  # index where the next non-zero element should go

    # Step 2: Iterate through the array with the right pointer
    for right in range(len(nums)):
        # Step 3: If the current element is non-zero, swap it with the element at the left pointer
        if nums[right] != 0:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1  # move the left pointer to the next position

```

### Edge Cases

1. **All Zeros**: If the array contains only zeros, the function should leave the array unchanged.
2. **No Zeros**: If the array contains no zeros, the function should leave the array unchanged.
3. **Zeros at the Beginning or End**: The function should correctly handle cases where zeros are already at the beginning or end.

### Unit Test

```python
import unittest

class TestMoveZeroes(unittest.TestCase):

    def test_no_zeroes(self):
        nums = [1, 2, 3]
        move_zeroes(nums)
        self.assertEqual(nums, [1, 2, 3])

    def test_all_zeroes(self):
        nums = [0, 0, 0]
        move_zeroes(nums)
        self.assertEqual(nums, [0, 0, 0])

    def test_mixed_elements(self):
        nums = [0, 1, 0, 3, 12]
        move_zeroes(nums)
        self.assertEqual(nums, [1, 3, 12, 0, 0])

    def test_zeros_at_end(self):
        nums = [1, 3, 12, 0, 0]
        move_zeroes(nums)
        self.assertEqual(nums, [1, 3, 12, 0, 0])

    def test_zeros_at_start(self):
        nums = [0, 0, 1, 3, 12]
        move_zeroes(nums)
        self.assertEqual(nums, [1, 3, 12, 0, 0])

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Alternative Approach

Another way to solve this problem is by first counting the number of zeros and then creating a new list with the non-zero elements followed by the counted zeros. However, this approach would use extra space, which contradicts the in-place requirement of the problem.

Thus, the two-pointer approach remains the best solution due to its optimal time complexity and in-place modification.