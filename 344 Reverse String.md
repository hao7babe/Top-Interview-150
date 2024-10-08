# 344. Reverse String

Difficulty: easy
Link: https://leetcode.com/problems/reverse-string
Topic: String

### Problem Analysis

The problem asks us to determine if two strings are anagrams of each other. Two strings are considered anagrams if they contain the same characters in the same frequency but potentially in a different order.

**Examples**:

- Input: `s = "anagram"`, `t = "nagaram"`
    - Output: `True`
- Input: `s = "rat"`, `t = "car"`
    - Output: `False`

### Approach

1. **Sorting**:
    - Sort both strings and compare them. If the sorted versions of the strings are identical, then the strings are anagrams.
    - This approach is straightforward but less efficient in terms of time complexity due to the sorting step.
2. **Frequency Count (Optimal Solution)**:
    - Use a dictionary (or an array of size 26 if the strings contain only lowercase English letters) to count the frequency of each character in both strings.
    - Compare the frequency counts. If they match for all characters, the strings are anagrams.

### Time and Space Complexity

- **Sorting Approach**:
    - **Time Complexity**: O(n log n), where n is the length of the strings (assuming the strings are of the same length).
    - **Space Complexity**: O(1) or O(n) depending on the implementation of the sort (if in-place or not).
- **Frequency Count Approach**:
    - **Time Complexity**: O(n), where n is the length of the strings.
    - **Space Complexity**: O(1) (if using an array of size 26) or O(n) (if using a dictionary, but since the space is bounded by the number of distinct characters, it's considered O(1) for fixed alphabets).

Given these considerations, the **Frequency Count Approach** is more efficient and is generally the preferred method.

### Code Implementation (Frequency Count Approach)

```python
def is_anagram(s, t):
    # Step 1: Edge case - if the lengths differ, they can't be anagrams
    if len(s) != len(t):
        return False

    # Step 2: Create a frequency dictionary for characters in the first string
    char_count = {}

    # Step 3: Count the frequency of each character in the first string
    for char in s:
        char_count[char] = char_count.get(char, 0) + 1

    # Step 4: Decrease the frequency for each character in the second string
    for char in t:
        if char in char_count:
            char_count[char] -= 1
            if char_count[char] == 0:
                del char_count[char]
        else:
            return False

    # Step 5: If the dictionary is empty, the strings are anagrams
    return len(char_count) == 0

```

### Edge Cases

1. **Different Lengths**: If the two strings have different lengths, they can't be anagrams.
2. **Empty Strings**: Two empty strings should be considered anagrams.
3. **Identical Strings**: A string should be an anagram of itself.

### Unit Test

```python
import unittest

class TestIsAnagram(unittest.TestCase):

    def test_basic_anagram(self):
        self.assertTrue(is_anagram("anagram", "nagaram"))

    def test_different_lengths(self):
        self.assertFalse(is_anagram("rat", "car"))

    def test_identical_strings(self):
        self.assertTrue(is_anagram("abc", "abc"))

    def test_empty_strings(self):
        self.assertTrue(is_anagram("", ""))

    def test_non_anagram(self):
        self.assertFalse(is_anagram("aabbcc", "aabbc"))

    def test_case_sensitivity(self):
        self.assertFalse(is_anagram("a", "A"))

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

### Alternative Approach (Sorting)

```python
def is_anagram(s, t):
    # Step 1: Sort both strings
    return sorted(s) == sorted(t)
```

While the sorting method is simpler to implement, the **Frequency Count Approach** is generally better in terms of performance, especially for larger strings. The sorting approach, while easy to understand, has a higher time complexity of O(n log n) compared to the O(n) of the frequency count method.