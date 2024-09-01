# 242. Valid Anagram

Difficulty: easy
Link: https://leetcode.com/problems/valid-anagram
Topic: String

```
**Example 1:**
Input: s = "anagram", t = "nagaram"
Output: true
**Example 2:**
Input: s = "rat", t = "car"
Output: false
```

### Questions

- Upper and lower case？

### Approach

**Hash Table:** tracking the count of each character

```python
count = defaultdict(int)

for x in s:
	count[x] += 1
for x in t:
	count[x] -= 1

for val in count.values():
	if val != 0:
		return False
		
return True
```

Time: $O(n)$, traverse the list once to count the frequency of the characters

Space: $O(1)$, fixed variable, 26 lowercase letters

### Alternatives

- sorting

```
**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?
```