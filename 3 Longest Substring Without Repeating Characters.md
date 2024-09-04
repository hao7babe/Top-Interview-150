# 3. Longest Substring Without Repeating Characters

Difficulty: Medium
Link: https://leetcode.com/problems/longest-substring-without-repeating-characters
Topic: String

### Problem Analysis

The problem asks us to find the length of the longest substring without repeating characters from a given string `s`. A substring is a contiguous sequence of characters within a string.

**Examples**:

- Input: `s = "abcabcbb"`
    - Output: `3` (the longest substring without repeating characters is `"abc"`)
- Input: `s = "bbbbb"`
    - Output: `1` (the longest substring without repeating characters is `"b"`)
- Input: `s = "pwwkew"`
    - Output: `3` (the longest substring without repeating characters is `"wke"`)

### Approach

We can solve this problem efficiently using the **Sliding Window** technique with a **Hash Set** to track characters in the current window. This allows us to maintain a window of non-repeating characters and expand or shrink the window as necessary.

1. **Sliding Window with Hash Set**:
    - We use two pointers (`left` and `right`) to define a sliding window.
    - As we expand the window by moving the `right` pointer, we add characters to a set.
    - If a character is already in the set, it means we have found a repeated character, so we shrink the window by moving the `left` pointer until the repeated character is removed from the set.
    - At each step, we track the maximum size of the window (i.e., the length of the substring).

### Time and Space Complexity

- **Time Complexity**: O(n), where `n` is the length of the string `s`. Each character is processed at most twice (once when added to the set and once when removed).
- **Space Complexity**: O(min(n, m)), where `n` is the length of the string, and `m` is the size of the character set (for example, 26 for lowercase English letters). We use extra space to store the characters in a set.

### Code Implementation

```python
def length_of_longest_substring(s):
    # Step 1: Initialize variables for tracking
    char_set = set()  # To track characters in the current window
    left = 0  # Left pointer of the sliding window
    max_len = 0  # The maximum length of a substring without repeating characters

    # Step 2: Iterate over the string with the right pointer
    for right in range(len(s)):
        # Step 3: If the character is already in the set, remove from left until no duplicate
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1

        # Step 4: Add the current character to the set
        char_set.add(s[right])

        # Step 5: Update the maximum length of the substring
        max_len = max(max_len, right - left + 1)

    # Step 6: Return the maximum length found
    return max_len

```

### Edge Cases

1. **Empty String**: If the input string is empty, the result should be `0`.
2. **All Repeating Characters**: If the string contains only one repeating character (e.g., `"bbbbb"`), the result should be `1`.
3. **Single Character String**: If the string contains only one character, the result should be `1`.

### Unit Test

```python
import unittest

class TestLengthOfLongestSubstring(unittest.TestCase):

    def test_basic_case(self):
        self.assertEqual(length_of_longest_substring("abcabcbb"), 3)

    def test_single_character_repeated(self):
        self.assertEqual(length_of_longest_substring("bbbbb"), 1)

    def test_mixed_characters(self):
        self.assertEqual(length_of_longest_substring("pwwkew"), 3)

    def test_empty_string(self):
        self.assertEqual(length_of_longest_substring(""), 0)

    def test_single_character(self):
        self.assertEqual(length_of_longest_substring("a"), 1)

    def test_all_unique_characters(self):
        self.assertEqual(length_of_longest_substring("abcdefg"), 7)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Alternative Approach (Using a Dictionary)

We can also solve the problem using a **Hash Map (Dictionary)** to store the most recent index of each character. This way, we can directly jump the `left` pointer to avoid reprocessing characters.

```python
def length_of_longest_substring(s):
    # Step 1: Initialize variables
    char_index = {}  # Dictionary to store the index of characters
    left = 0  # Left pointer
    max_len = 0  # Maximum length

    # Step 2: Iterate through the string with the right pointer
    for right, char in enumerate(s):
        # Step 3: If the character is in the dictionary and its index is greater or equal to left, move the left pointer
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1

        # Step 4: Update the character's index in the dictionary
        char_index[char] = right

        # Step 5: Calculate the maximum length
        max_len = max(max_len, right - left + 1)

    # Step 6: Return the maximum length
    return max_len

```

### Summary

- The **Sliding Window Approach** with a Hash Set or Hash Map is an efficient solution with O(n) time complexity.
- Both the Hash Set and Hash Map methods are effective, but the Hash Map approach can potentially move the left pointer faster in certain cases.
- The algorithm handles edge cases, such as empty strings and strings with repeating characters.