# 242. Valid Anagram

Difficulty: easy
Link: https://leetcode.com/problems/valid-anagram
Topic: String

### Problem Analysis

The problem requires us to determine if two strings are anagrams of each other. Two strings are considered anagrams if they contain the exact same characters in the exact same frequency, but the order of the characters can be different.

**Examples**:

- Input: `s = "anagram"`, `t = "nagaram"`
    - Output: `True`
- Input: `s = "rat"`, `t = "car"`
    - Output: `False`

### Approach

To solve this problem efficiently, we can use the following approach:

1. **Frequency Count (Optimal Solution)**:
    - Use a dictionary to count the frequency of each character in both strings.
    - Compare the frequency counts for both strings. If they match for all characters, the strings are anagrams.
2. **Sorting (Alternative Solution)**:
    - Sort both strings and compare them. If the sorted versions of the strings are identical, then the strings are anagrams.
    - This method is straightforward but less efficient than the frequency count approach.

### Time and Space Complexity

- **Frequency Count Approach**:
    - **Time Complexity**: O(n), where n is the length of the strings (assuming the strings are of the same length).
    - **Space Complexity**: O(1) if we consider the number of possible characters (26 lowercase letters) as constant.
- **Sorting Approach**:
    - **Time Complexity**: O(n log n), where n is the length of the strings.
    - **Space Complexity**: O(n), due to the space required to store the sorted versions of the strings.

Given these considerations, the **Frequency Count Approach** is more efficient and is generally preferred.

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
4. **Case Sensitivity**: The solution assumes that the problem is case-sensitive unless specified otherwise.

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
    # Step 1: Sort both strings and compare
    return sorted(s) == sorted(t)

```

### Summary

- The **Frequency Count Approach** is optimal due to its O(n) time complexity and O(1) space complexity when considering a fixed character set.
- The **Sorting Approach** is simpler but less efficient with a time complexity of O(n log n). This approach can be used for smaller strings or when simplicity is more important than performance.