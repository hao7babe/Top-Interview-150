# 14. Longest Common Prefix

Difficulty: easy
Link: https://leetcode.com/problems/longest-common-prefix
Topic: String

### Problem Analysis

The problem asks us to find the longest common prefix among a set of strings. If no common prefix exists, we should return an empty string `""`.

**Key Considerations**:

- The common prefix must be shared among all strings in the array.
- If the array is empty, the output should be an empty string.
- If there’s no common prefix, the result should also be an empty string.

**Examples**:

- Input: `["flower", "flow", "flight"]`, Output: `"fl"`.
- Input: `["dog", "racecar", "car"]`, Output: `""`.

### Approach

1. **Horizontal Scanning**: Start with the first string as the prefix and compare it with each subsequent string, shortening the prefix as necessary.
2. **Vertical Scanning**: Compare characters column by column across all strings until we find a mismatch or reach the end of one string.
3. **Divide and Conquer**: Recursively divide the array of strings, find the longest common prefix for each half, and then combine them.

### Complexity Analysis

1. **Horizontal Scanning:**
    - **Time**: O(S), where S is the sum of all characters in the input strings.
    - **Space**: O(1) (only uses constant extra space).
2. **Vertical Scanning**:
    - **Time**: O(S), similar to horizontal scanning.
    - **Space**: O(1) (only uses constant extra space).
3. **Divide and Conquer**:
    - **Time:** O(S * log N), where N is the number of strings.
    - **Space**: O(m * log N), where m is the length of the common prefix due to recursion stack.

Given these complexities, **vertical scanning** is a strong choice due to its simplicity and efficiency (O(S) time, O(1) space), making it easy to implement and understand. 

### Code Implementation

```python
def longestCommonPrefix(strs):
    # Step 1: Return empty string if input array is empty
    if not strs:
        return ""

    # Step 2: Iterate over the characters of the first string
    for i in range(len(strs[0])):
        char = strs[0][i]  # Use the i-th character of the first string as a reference

        # Step 3: Compare this character with the same position in all other strings
        for s in strs[1:]:
            # Check two conditions: if we've reached the end of a string or if characters don't match
            if i == len(s) or s[i] != char:
                # Return the substring up to the mismatch point
                return strs[0][:i]

    # Step 4: If no mismatch was found, the first string is the common prefix
    return strs[0]

```

### Dry Run

Let's manually test this code with a few examples to ensure correctness.

### Example 1:

Input: `["flower", "flow", "flight"]`

1. **Initial Check**:
    - The array is not empty, so we proceed.
2. **Column 0**:
    - Reference character is `'f'`. All strings (`"flow"`, `"flight"`) have `'f'` at index 0. Continue.
3. **Column 1**:
    - Reference character is `'l'`. All strings have `'l'` at index 1. Continue.
4. **Column 2**:
    - Reference character is `'o'`. The third string (`"flight"`) has `'i'` at index 2, which is a mismatch. Return `"fl"`.

Output: `"fl"`

### Example 2:

Input: `["dog", "racecar", "car"]`

1. **Initial Check**:
    - The array is not empty, so we proceed.
2. **Column 0**:
    - Reference character is `'d'`. The second string (`"racecar"`) has `'r'` at index 0, which is a mismatch. Return `""`.

Output: `""`

### Conclusion

This vertical scanning approach is efficient, especially when there are only a few strings or when the common prefix is short. It stops as soon as it detects a mismatch, making it faster than methods that might compare longer substrings unnecessarily. The code handles edge cases like empty arrays or strings of different lengths appropriately.

### Alternatives

- Vertical Scanning Approach

```python

def longestCommonPrefix(strs):
    # Step 1: Handle the edge case where the input list is empty
    if not strs:
        return ""
    
    # Step 2: Iterate over each character in the first string (strs[0])
    for i in range(len(strs[0])):
        # Take the i-th character of the first string as the reference character
        char = strs[0][i]
        
        # Step 3: Compare this character with the corresponding character in all other strings
        for s in strs[1:]:
            # If the current string is shorter or the character doesn't match, return the prefix up to this point
            if i == len(s) or s[i] != char:
                return strs[0][:i]
    
    # Step 4: If no mismatch is found after comparing all characters, the first string itself is the common prefix
    return strs[0]

```

- Divide and Conquer Approach

```python
def longestCommonPrefix(strs):
    # Step 1: Handle the edge case where the input list is empty
    if not strs:
        return ""
    
    # Step 2: Define a helper function that compares two strings and finds their common prefix
    def commonPrefix(left, right):
        # Determine the minimum length between the two strings
        min_len = min(len(left), len(right))
        
        # Compare characters up to the minimum length
        for i in range(min_len):
            if left[i] != right[i]:
                return left[:i]
        
        # If all characters match up to the min_len, return the entire common part
        return left[:min_len]
    
    # Step 3: Define the divide and conquer function
    def divideAndConquer(strs, l, r):
        # Base case: if there's only one string in the range, return it
        if l == r:
            return strs[l]
        else:
            # Divide the range into two halves
            mid = (l + r) // 2
            
            # Recursively find the common prefix in the left half and right half
            lcpLeft = divideAndConquer(strs, l, mid)
            lcpRight = divideAndConquer(strs, mid + 1, r)
            
            # Combine the results by finding the common prefix between the two halves
            return commonPrefix(lcpLeft, lcpRight)
    
    # Step 4: Call the divide and conquer function on the full range of the input list
    return divideAndConquer(strs, 0, len(strs) - 1)
```