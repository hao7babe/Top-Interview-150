# 28. Find the Index of the First Occurrence in a String

Difficulty: easy
Link: https://leetcode.com/problems/implement-strstr
Topic: String

### Problem Analysis

The problem asks to find the index of the first occurrence of a substring (`needle`) within another string (`haystack`). If `needle` is not found within `haystack`, the function should return `-1`.

This is similar to the functionality of Python's built-in `str.find()` method or the `indexOf()` method in other languages.

**Examples**:

- Input: `haystack = "sadbutsad"`, `needle = "sad"`
    - Output: `0` (the first occurrence of "sad" starts at index 0)
- Input: `haystack = "leetcode"`, `needle = "leeto"`
    - Output: `1` (since "leeto" is not found in "leetcode")

### Approach

1. **Simple Sliding Window**:
    - We can iterate over the `haystack` string with a sliding window approach. For each index `i`, we check if the substring from `i` to `i + len(needle)` matches `needle`.
    - If a match is found, return the index `i`.
    - If the loop completes without finding a match, return `1`.
2. **Edge Cases**:
    - If `needle` is an empty string, return `0` (since an empty string is trivially found at the start of any string).
    - If `needle` is longer than `haystack`, return `1` (since it cannot be found).

### Time and Space Complexity

- **Time Complexity**: O(m * n), where `m` is the length of `needle` and `n` is the length of `haystack`. In the worst case, we might have to compare the substring of length `m` for every position in the `haystack`.
- **Space Complexity**: O(1), as we are not using any extra space except for a few variables.

### Edge Cases

1. **Empty `needle`**: If `needle` is empty, return `0`, as the problem usually defines that an empty string is always found at index `0`.
2. **Needle longer than haystack**: If `needle` is longer than `haystack`, return `1`, since `needle` cannot be found in `haystack`.
3. **Identical strings**: If `haystack` is identical to `needle`, return `0`, since the entire `haystack` starts at index `0`.

### Code Implementation

```python
def strStr(haystack, needle):
    # Step 1: Handle the edge case where needle is empty
    if not needle:
        return 0

    # Step 2: Get the lengths of both strings
    len_haystack, len_needle = len(haystack), len(needle)

    # Step 3: Iterate over the haystack using a sliding window
    for i in range(len_haystack - len_needle + 1):
        # Step 4: Check if the substring starting at i matches the needle
        if haystack[i:i + len_needle] == needle:
            return i

    # Step 5: If no match is found, return -1
    return -1
```

### Unit Test

```python
import unittest

class TestStrStr(unittest.TestCase):

    def test_basic_match(self):
        self.assertEqual(strStr("sadbutsad", "sad"), 0)

    def test_no_match(self):
        self.assertEqual(strStr("leetcode", "leeto"), -1)

    def test_empty_needle(self):
        self.assertEqual(strStr("abc", ""), 0)

    def test_needle_longer_than_haystack(self):
        self.assertEqual(strStr("abc", "abcd"), -1)

    def test_identical_strings(self):
        self.assertEqual(strStr("abc", "abc"), 0)

    def test_match_at_end(self):
        self.assertEqual(strStr("hello", "lo"), 3)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Summary

- The sliding window approach efficiently checks for the first occurrence of `needle` in `haystack`.
- The edge cases of an empty `needle` and the case where `needle` is longer than `haystack` are handled explicitly.
- This solution runs in O(n * m) time complexity, which is reasonable for small to medium-sized strings.