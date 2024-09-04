# 189. Rotate Array

Difficulty: Medium
Link: https://leetcode.com/problems/rotate-array
Topic: Array

### Problem Analysis

The problem asks us to rotate an array of integers to the right by `k` steps. Each element in the array is shifted `k` positions to the right, with the elements that are displaced from the end wrapping around to the beginning of the array.

**Examples**:

- Input: `nums = [1,2,3,4,5,6,7]`, `k = 3`
    - Output: `[5,6,7,1,2,3,4]`
    - Explanation: After rotating the array 3 steps to the right, the elements `5, 6, 7` move to the front.
- Input: `nums = [-1,-100,3,99]`, `k = 2`
    - Output: `[3,99,-1,-100]`

### Approach

There are several ways to approach this problem:

1. **Using Extra Array**:
    - We can create a new array, place elements in their new positions, and then copy the new array back to the original array. However, this approach requires extra space.
2. **In-Place Rotation (Optimal Approach)**:
    - **Reverse the entire array**.
    - **Reverse the first `k` elements**.
    - **Reverse the remaining elements**.
    - This approach rotates the array in place without using extra space and works in O(n) time.

### Explanation of the In-Place Approach:

1. Reverse the entire array.
    - `nums = [1,2,3,4,5,6,7]` becomes `nums = [7,6,5,4,3,2,1]`.
2. Reverse the first `k` elements.
    - After reversing the first 3 elements (`k = 3`), `nums = [5,6,7,4,3,2,1]`.
3. Reverse the rest of the elements.
    - After reversing the elements from index `k` to the end, `nums = [5,6,7,1,2,3,4]`.

### Time and Space Complexity

- **Time Complexity**: O(n), where `n` is the length of the array, since we perform three reversals.
- **Space Complexity**: O(1), as we modify the array in place without using extra memory.

### Edge Cases

1. **`k` larger than the array length**: The rotation count `k` should be reduced by taking `k % len(nums)`, since rotating by `len(nums)` or any multiple of it will result in the same array.
2. **Empty Array**: If the array is empty, there is nothing to rotate, so return immediately.
3. **Single Element Array**: If the array contains only one element, rotating it any number of times does not change the array.

### Code Implementation

```python
def rotate(nums, k):
    # Step 1: Normalize k in case it's larger than the length of the array
    k = k % len(nums)

    # Step 2: Helper function to reverse a portion of the array
    def reverse(nums, start, end):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
            end -= 1

    # Step 3: Reverse the entire array
    reverse(nums, 0, len(nums) - 1)

    # Step 4: Reverse the first k elements
    reverse(nums, 0, k - 1)

    # Step 5: Reverse the remaining elements
    reverse(nums, k, len(nums) - 1)

```

### Unit Test

```python
import unittest

class TestRotateArray(unittest.TestCase):

    def test_basic_rotation(self):
        nums = [1, 2, 3, 4, 5, 6, 7]
        rotate(nums, 3)
        self.assertEqual(nums, [5, 6, 7, 1, 2, 3, 4])

    def test_k_greater_than_length(self):
        nums = [1, 2, 3, 4, 5]
        rotate(nums, 7)  # Equivalent to rotating by 2
        self.assertEqual(nums, [4, 5, 1, 2, 3])

    def test_single_element(self):
        nums = [1]
        rotate(nums, 10)
        self.assertEqual(nums, [1])

    def test_empty_array(self):
        nums = []
        rotate(nums, 5)
        self.assertEqual(nums, [])

    def test_full_rotation(self):
        nums = [1, 2, 3, 4, 5]
        rotate(nums, 5)  # Full rotation returns the same array
        self.assertEqual(nums, [1, 2, 3, 4, 5])

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Alternative Approach (Using Extra Array)

```python
def rotate(nums, k):
    n = len(nums)
    k = k % n  # Normalize k
    nums[:] = nums[-k:] + nums[:-k]  # Create a new rotated array and assign it back

```

### Summary

- The **In-Place Rotation Approach** is optimal, modifying the array in place in O(n) time and O(1) space.
- We handle various edge cases, including when `k` is larger than the length of the array, single-element arrays, and empty arrays.