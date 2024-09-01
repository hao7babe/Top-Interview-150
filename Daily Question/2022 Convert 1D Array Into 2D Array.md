# 2022. Convert 1D Array Into 2D Array

day: September 1, 2024
link: https://leetcode.com/problems/convert-1d-array-into-2d-array/description/?envType=daily-question&envId=2024-09-01

```
**Example 1:**
Input: original = [1,2,3,4], m = 2, n = 2
Output: [[1,2],[3,4]]
Explanation: The constructed 2D array should contain 2 rows and 2 columns.
The first group of n=2 elements in original, [1,2], becomes the first row in the constructed 2D array.
The second group of n=2 elements in original, [3,4], becomes the second row in the constructed 2D array.
**Example 2:**
Input: original = [1,2,3], m = 1, n = 3
Output: [[1,2,3]]
Explanation: The constructed 2D array should contain 1 row and 3 columns.
Put all three elements in original into the first row of the constructed 2D array.
```

### Approach

- Use a two-tier loop, with the outer loop taking care of the rows and the inner loop taking care of the columns.
- In each loop, the element at the corresponding position is removed from the original and placed into a two-dimensional array.

```python
  if len(original) != m * n:
      return []
  
  result = []
  for i in range(m):
      row = original[i * n:(i + 1) * n]
      result.append(row)
  
  return result
```

Time complexity: $O(m * n)$, go through m * n elements to fill the 2D array.

Space complexity: $O(1)$, aside from the returned 2D array, only used a constant amount of extra space.