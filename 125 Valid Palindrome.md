# 125. Valid Palindrome

Difficulty: easy
Link: https://leetcode.com/problems/valid-palindrome
Topic: String

### Problem Analysis

To determine if a given string is a palindrome, considering only alphanumeric characters and ignoring cases. A string is a palindrome if it reads the same forward and backward.

**Examples**:

- Input: `"A man, a plan, a canal: Panama"`, Output: `True`
- Input: `"race a car"`, Output: `False`

### Approach

1. **Two-Pointer Approach**: This is the most efficient way to check if the string is a palindrome by using two pointers starting from the beginning and end of the string, moving towards the center while skipping non-alphanumeric characters.
2. **String Cleaning and Reverse Comparison**: Another way is to clean the string by removing non-alphanumeric characters, converting it to lower case, and then comparing it with its reverse.

### Time and Space Complexity

- **Two-Pointer Approach**:
    - **Time Complexity**: O(n), where n is the length of the string. Each character is processed at most once.
    - **Space Complexity**: O(1), no additional space is required other than a few variables.
- **String Cleaning and Reverse Comparison**:
    - **Time Complexity**: O(n), where n is the length of the string. The string is processed to remove non-alphanumeric characters and then compared.
    - **Space Complexity**: O(n), because a new string is created after cleaning.

Given the problem's requirements and the constraints, the **Two-Pointer Approach** is more space-efficient, so we will implement that.

### Code Implementation

```python

def isPalindrome(s):
    # Step 1: Initialize two pointers, left at the start and right at the end of the string
    left, right = 0, len(s) - 1

    # Step 2: Loop until the pointers cross each other
    while left < right:
        # Step 3: Move the left pointer to the right until an alphanumeric character is found
        while left < right and not s[left].isalnum():
            left += 1

        # Step 4: Move the right pointer to the left until an alphanumeric character is found
        while left < right and not s[right].isalnum():
            right -= 1

        # Step 5: Compare the characters at left and right pointers (ignoring case)
        if s[left].lower() != s[right].lower():
            return False

        # Step 6: Move both pointers towards the center
        left += 1
        right -= 1

    # Step 7: If all characters matched, the string is a palindrome
    return True
```

### Edge Cases

1. **Empty String**: An empty string should return `True` because technically, it reads the same forward and backward.
2. **String with Only Non-Alphanumeric Characters**: Strings like `"!!!"` should return `True` because if you remove all non-alphanumeric characters, you're left with an empty string.
3. **String with a Single Character**: A single character should return `True` because it reads the same forward and backward.

### Unit Test

```python

def test_empty_string(self):
    self.assertTrue(isPalindrome(""))

def test_only_non_alphanumeric(self):
    self.assertTrue(isPalindrome("!!!"))

def test_single_character(self):
    self.assertTrue(isPalindrome("a"))
    self.assertTrue(isPalindrome("Z"))

def test_mixed_case_and_symbols(self):
    self.assertTrue(isPalindrome("A man, a plan, a canal: Panama"))

def test_no_palindromic_properties(self):
    self.assertFalse(isPalindrome("abc"))
    self.assertFalse(isPalindrome("race a car"))

def test_numeric_palindrome(self):
    self.assertTrue(isPalindrome("12321"))
    self.assertTrue(isPalindrome("12 3 21"))
    self.assertFalse(isPalindrome("123456"))

if __name__ == "__main__":
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

### Alternative

```python

def isPalindrome(s):
    # Step 1: Clean the string by removing non-alphanumeric characters and converting to lower case
    cleaned = ''.join(char.lower() for char in s if char.isalnum())

    # Step 2: Compare the cleaned string with its reverse
    return cleaned == cleaned[::-1]
```