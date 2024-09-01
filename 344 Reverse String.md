# 344. Reverse String

Difficulty: easy
Link: https://leetcode.com/problems/reverse-string
Topic: String

```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

with O(1) extra memory.
```

### Approach

Use two pointers to switch letters from right to left side.

```python
l, r = 0, len(s) - 1
while l < r:
	s[l], s[r] = s[r], s[l]
	l += 1
	r -= 1 
```

Time: $O(n)$, The loop is executed n/2 times

Space: $O(1)$, input s and fixed two additional pointer variables