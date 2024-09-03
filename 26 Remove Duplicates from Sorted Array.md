# 26. Remove Duplicates from Sorted Array

Difficulty: easy
Link: https://leetcode.com/problems/remove-duplicates-from-sorted-array
Topic: Array

### Problem Analysis

The problem asks us to remove duplicates from a sorted array in-place and return the length of the modified array. Since the array is sorted, duplicates will be consecutive. The goal is to move the unique elements to the beginning of the array, leaving the rest of the array unchanged. The result should be the length of the unique portion of the array.

**Examples**:

- Input: `nums = [1,1,2]`
    - Output: `2`, `nums = [1,2,_]` (the first two elements are the unique elements, the `_` denotes the part of the array we don’t care about).
- Input: `nums = [0,0,1,1,1,2,2,3,3,4]`
    - Output: `5`, `nums = [0,1,2,3,4,_,_,_,_,_]`

### Approach

Since the array is sorted, we can use a two-pointer technique to efficiently remove duplicates.

1. **Two-Pointer Technique**: We use one pointer (`i`) to track the position in the new array where the next unique element should go. The other pointer (`j`) scans through the array. When `nums[j]` is different from the previous unique element (`nums[i-1]`), we move `nums[j]` to `nums[i]` and increment `i`.

### Time and Space Complexity

- **Time Complexity**: O(n), where n is the length of the array. We make a single pass through the array.
- **Space Complexity**: O(1), since we are modifying the array in place and using only a constant amount of extra space.

### Code Implementation

```python
def remove_duplicates(nums):
    # Step 1: Edge case - if the array is empty, return 0
    if not nums:
        return 0

    # Step 2: Initialize the first pointer
    i = 1  # index where the next unique element should go

    # Step 3: Iterate through the array with the second pointer
    for j in range(1, len(nums)):
        # Step 4: If current element is different from the previous unique element
        if nums[j] != nums[i - 1]:
            nums[i] = nums[j]  # move it to the 'unique' position
            i += 1  # move the 'unique' pointer

    # Step 5: Return the length of the unique elements
    return i

```

### Edge Cases

1. **Empty Array**: If the input array is empty, the function should return `0`.
2. **Array with No Duplicates**: If there are no duplicates, the function should return the length of the original array.
3. **Array with All Duplicates**: If all elements are the same, the function should return `1`.

### Unit Test

```python
import unittest

class TestRemoveDuplicates(unittest.TestCase):

    def test_empty_array(self):
        self.assertEqual(remove_duplicates([]), 0)

    def test_single_element(self):
        self.assertEqual(remove_duplicates([1]), 1)

    def test_no_duplicates(self):
        self.assertEqual(remove_duplicates([1, 2, 3]), 3)

    def test_with_duplicates(self):
        self.assertEqual(remove_duplicates([1, 1, 2]), 2)
        self.assertEqual(remove_duplicates([0,0,1,1,1,2,2,3,3,4]), 5)

    def test_all_duplicates(self):
        self.assertEqual(remove_duplicates([2, 2, 2, 2, 2]), 1)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```