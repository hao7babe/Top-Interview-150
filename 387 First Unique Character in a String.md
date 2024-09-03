# 387. First Unique Character in a String

Difficulty: easy
Link: https://leetcode.com/problems/first-unique-character-in-a-string
Topic: String

### Problem Analysis

The problem requires finding the first non-repeating character in a string and returning its index. If no such character exists, the function should return `-1`.

**Examples**:

- Input: `"leetcode"`, Output: `0` (The first unique character is `'l'` at index `0`.)
- Input: `"loveleetcode"`, Output: `2` (The first unique character is `'v'` at index `2`.)
- Input: `"aabb"`, Output: `1` (There are no unique characters.)

### Approach

1. **Frequency Count Using a Dictionary**:
    - Traverse the string once to build a frequency count for each character.
    - Traverse the string a second time to find the first character with a frequency of 1.
2. **Single Pass with Array**:
    - Use an array to store the count of each character (assuming the character set is small, like ASCII).
    - Traverse the string to update the array, and then traverse the string again to find the first unique character.

### Time and Space Complexity

- **Frequency Count Approach**:
    - **Time Complexity**: O(n), where n is the length of the string. This is because we traverse the string twice.
    - **Space Complexity**: O(1) if we consider the space used by the dictionary to be constant (bounded by the character set size, e.g., 26 for lowercase English letters). Otherwise, it's O(n).

Given the constraints and the fact that we're dealing with a small set of characters, the **Frequency Count Approach** is both time-efficient and easy to implement.

### Code Implementation

```python
def firstUniqChar(s):
    # Step 1: Create a dictionary to store the frequency of each character
    char_count = {}

    # Step 2: Populate the dictionary with character counts
    for char in s:
        char_count[char] = char_count.get(char, 0) + 1

    # Step 3: Find the first character with a count of 1
    for index, char in enumerate(s):
        if char_count[char] == 1:
            return index

    # Step 4: If no unique character is found, return -1
    return -1

```

### Edge Cases

1. **Empty String**: An empty string should return `1` since there are no characters to consider.
2. **All Repeating Characters**: A string where every character repeats should return `1`.
3. **Single Character**: A string with a single character should return `0` since it's unique by default.
4. **String with Multiple Unique Characters**: The function should correctly identify and return the index of the first one.

### Unit Test

```python
import unittest

class TestFirstUniqChar(unittest.TestCase):

    def test_basic(self):
        self.assertEqual(firstUniqChar("leetcode"), 0)
        self.assertEqual(firstUniqChar("loveleetcode"), 2)

    def test_all_repeating(self):
        self.assertEqual(firstUniqChar("aabbcc"), -1)

    def test_single_character(self):
        self.assertEqual(firstUniqChar("z"), 0)

    def test_empty_string(self):
        self.assertEqual(firstUniqChar(""), -1)

    def test_longer_string(self):
        self.assertEqual(firstUniqChar("abcdabcdabcdabcde"), 16)

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)

```

### Alternative Approach

An alternative approach could involve using an array instead of a dictionary, especially if we know the character set is small (e.g., ASCII). Here's how it would look:

```python
def firstUniqChar(s):
    # Step 1: Create an array to store frequency counts of characters
    char_count = [0] * 26  # Assuming lowercase English letters

    # Step 2: Populate the array with counts (map 'a' to index 0, 'z' to index 25)
    for char in s:
        char_count[ord(char) - ord('a')] += 1

    # Step 3: Find the first character with a count of 1
    for index, char in enumerate(s):
        if char_count[ord(char) - ord('a')] == 1:
            return index

    # Step 4: If no unique character is found, return -1
    return -1

```

This approach can be slightly faster and more space-efficient when working with a small, fixed character set like lowercase English letters.