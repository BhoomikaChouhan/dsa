---

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

### Example 1:

**Input:** `nums = [-1,0,1,2,-1,-4]`  
**Output:** `[[-1,-1,2],[-1,0,1]]`  
**Explanation:** 
- `nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0`
- `nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0`
- `nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0`
- The distinct triplets are `[-1,0,1]` and `[-1,-1,2]`.
- Notice that the order of the output and the order of the triplets does not matter.

### Example 2:

**Input:** `nums = [0,1,1]`  
**Output:** `[]`  
**Explanation:** The only possible triplet does not sum up to `0`.

### Example 3:

**Input:** `nums = [0,0,0]`  
**Output:** `[[0,0,0]]`  
**Explanation:** The only possible triplet sums up to `0`.

### Constraints:

- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

---
### `threeSum` Problem

**Objective**: Given an array `a`, find all unique triplets `[a[i], a[j], a[k]]` such that `i != j`, `i != k`, `j != k`, and `a[i] + a[j] + a[k] == 0`.

### Approach

1. **Sort the Array**:
   - Sorting helps to use a two-pointer technique efficiently.
   - Time Complexity for sorting: `O(n log n)`

2. **Iterate with Fixed First Element**:
   - Use the outer loop to fix the first element of the triplet.

3. **Two-Pointer Technique**:
   - For each fixed element, use two pointers to find pairs that sum to the negative of the fixed element.

4. **Avoid Duplicates**:
   - Skip duplicates to ensure unique triplets.

### Code Explanation

```java
class Solution {
    public List<List<Integer>> threeSum(int[] a) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(a);  // Step 1: Sort the array
        int n = a.length;
        
        for (int i = 0; i < n; i++) {
            if (i != 0 && a[i] == a[i - 1]) {
                continue;  // Step 4: Skip duplicate elements
            }

            int j = i + 1;  // Left pointer
            int k = n - 1;  // Right pointer

            while (j < k) {
                int sum = a[i] + a[j] + a[k];

                if (sum < 0) {
                    j++;  // Move left pointer right to increase sum
                } else if (sum > 0) {
                    k--;  // Move right pointer left to decrease sum
                } else {
                    ans.add(Arrays.asList(a[i], a[j], a[k]));  // Found a triplet
                    j++;
                    k--;

                    while (j < k && a[j] == a[j - 1]) {
                        j++;  // Skip duplicate elements
                    }
                    while (j < k && a[k] == a[k + 1]) {
                        k--;  // Skip duplicate elements
                    }
                }
            }
        }
        
        return ans;  // Return the list of unique triplets
    }
}
```

### Complexity

- **Time Complexity**:
  - Sorting: `O(n log n)`
  - Iterating with Two Pointers: `O(n^2)`
  - Overall: `O(n^2)`

- **Space Complexity**:
  - Result list storage: `O(n^2)` (in the worst case with many unique triplets)
  - Sorting in place: `O(1)`

### Dry Run

**Example**: `a = [-1, 0, 1, 2, -1, -4]`

1. **Sorted Array**: `[-4, -1, -1, 0, 1, 2]`

2. **Fixed Element**: `a[i] = -4`
   - Two-pointer: `j = -1`, `k = 2`
   - Sum: `-4 + (-1) + 2 = -3` (Less than 0, increment `j`)

3. **Next Pointers**:
   - Sum: `-4 + (-1) + 2 = -3` (Continue incrementing `j` until sum `>= 0`)

4. **Fixed Element**: `a[i] = -1`
   - Two-pointer: `j = -1`, `k = 2`
   - Sum: `-1 + (-1) + 2 = 0` (Valid triplet `[-1, -1, 2]`)
   - Skip duplicates: `j++`, `k--`

5. **Next**:
   - Continue this process until all elements are processed.

### Summary

- **Fixed Element Approach**: Helps to efficiently find the triplets.
- **Two-pointer Technique**: Reduces complexity from `O(n^3)` to `O(n^2)`.
- **Duplicate Handling**: Ensures all triplets are unique.
