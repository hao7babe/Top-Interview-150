# 26. Remove Duplicates from Sorted Array

Difficulty: easy
Link: https://leetcode.com/problems/remove-duplicates-from-sorted-array
Topic: Array

```
**Example 1：**
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

**Example 2：**
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

### Question：

- nums sorted in decreasing order?
- nums.length range?

### Approach：Two-pointer

In-Place Modification: Use one pointer (`slow`) to keep track of the position for the next unique element while using the other pointer (`fast`) to explore the array. By checking and copying elements only when necessary, the algorithm ensures that the array is compacted with all unique elements at the beginning.

```python
if not nums:
	return 0

slow = 0

for fast in range(1, len(nums)):
	if nums[fast] != nums[slow]:
		slow += 1
		nums[slow] = nums[fast]
		
return slow + 1
```

Time: $O(n)$, traverse the list once

Space: $O(1)$, fixed variable