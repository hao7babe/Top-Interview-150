# 1. Two Sum

Difficulty: easy
Link: https://leetcode.com/problems/two-sum
Topic: Array

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### **Edge cases, What if:**

- empty input
- only one input
- multi valid answer exists

### **1. Brute Force: Nested Loop**

Loop through each element x, and find if there is another value that equals to target - x

```python
for i in range(len(nums)):
	for j in range(i + 1, len(nums)):
		if nums[j] == target - nums[i]:
			return[i, j]
```

Time: $O(n^2)$, nested loop

Space: $O(1)$,  no storage

### 2. Trade space for time: Hash table

Use hash table to maintain a mapping of element value to index;

For fast Lookup, key == num[i], value == index

```python
hashmap = {}
for i in range(len(nums)):
    hashmap [nums[i]] = i
for i  in range(len(nums)):
    match = target - nums[i]
    if match in hashmap and hashmap[match] != i:
        return [i, hashmap[match]]
```

Time: $O(n)$, traverse the list twice

Space: $O(n)$, stores exactly *n* elements

### 3. Single traversal — Best Solution

```python
hashmap = {}
for i in range(len(nums)):
    match = target - nums[i]
    if match in hashmap:
        return [i, hashmap[match]]
    hashmap[nums[i]] = i
```

Time: $O(n)$, traverse the list once

Space: $O(n)$, stores at most *n* elements