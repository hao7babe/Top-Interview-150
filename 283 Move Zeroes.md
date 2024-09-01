# 283. Move Zeroes

Difficulty: easy
Link: https://leetcode.com/problems/move-zeroes
Topic: Array

```
Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

### Approach

Walk through nums with two pointers, switch pointers if the fast  pointer is not pointing to 0, all non-zero elements will be moved to the front of the array, and the rest will be filled with zeros.

```python
slow = 0
for fast in range(len(nums)):
	if nums[fast] != 0:
		nums[slow], nums[fast] = nums[fast], nums[slow]
		slow += 1
```

Time: $O(n)$, traverse the list once

Space: $O(1)$, fixed variable