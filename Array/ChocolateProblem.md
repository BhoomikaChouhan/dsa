### Problem Statement:

Given an array `A[]` of positive integers of size `N`, where each value represents the number of chocolates in a packet. Each packet can have a variable number of chocolates. There are `M` students, the task is to distribute chocolate packets among `M` students such that:
1. Each student gets exactly one packet.
2. The difference between the maximum number of chocolates given to a student and the minimum number of chocolates given to a student is minimum.

#### Example 1:
**Input**:
- `N = 8`
- `M = 5`
- `A = {3, 4, 1, 9, 56, 7, 9, 12}`

**Output**:
- `6`

**Explanation**:
- The minimum difference between maximum chocolates and minimum chocolates is `9 - 3 = 6` by choosing the following `M` packets: `{3, 4, 9, 7, 9}`.

#### Example 2:
**Input**:
- `N = 7`
- `M = 3`
- `A = {7, 3, 2, 4, 9, 12, 56}`

**Output**:
- `2`

**Explanation**:
- The minimum difference between maximum chocolates and minimum chocolates is `4 - 2 = 2` by choosing the following `M` packets: `{3, 2, 4}`.

### Task:

You don't need to take any input or print anything. Your task is to complete the function `findMinDiff()` which takes array `A[]`, `N`, and `M` as input parameters and returns the minimum possible difference between the maximum number of chocolates given to a student and the minimum number of chocolates given to a student.

### Expected Time Complexity: 
- `O(N*Log(N))`

### Expected Auxiliary Space: 
- `O(1)`

### Constraints:
- `1 ≤ T ≤ 100`
- `1 ≤ N ≤ 105`
- `1 ≤ Ai ≤ 109`
- `1 ≤ M ≤ N`


Bilkul! Is Java program ka purpose ye hai ki ek array ke andar se m elements ka subset nikala jaye jiska difference (maximum element - minimum element) sabse kam ho. Ab main isse point-wise, time complexity, space complexity aur dry run ke saath samjhata hoon:

### Point-wise Explanation:

1. **Function Definition**:
   - `findMinDiff` method ek `ArrayList<Integer>` `a`, ek integer `n` (array ki size), aur ek integer `m` (subset size) leta hai.

2. **Sort the Array**:
   - `Collections.sort(a)` ke use se, array ko ascending order mein sort kar diya jata hai.

3. **Initialize Variables**:
   - `min` ko `Integer.MAX_VALUE` se initialize kiya jata hai, jo sabse bada possible integer value hai.
   - `j` ko `m-1` se initialize kiya jata hai, jo subset ke end index ko denote karta hai.

4. **Loop Through Array**:
   - For loop start hota hai jo array ke har subset ko check karta hai jo length `m` ka hai.
   - `min` ko update kiya jata hai, jahan `Math.min(min, a.get(j) - a.get(i))` calculate karta hai current minimum difference ko.
   - `i` aur `j` pointers ko accordingly move karte hain next subset ko check karne ke liye.

5. **Return Minimum Difference**:
   - Loop complete hone ke baad, `min` ko return karte hain, jo sabse chhota possible difference hai jo humne find kiya.

### Time Complexity:
- **Sorting the Array**: `O(n log n)`
- **Loop through Array**: `O(n)`

Total time complexity: `O(n log n)`

### Space Complexity:
- **Space Complexity**: `O(1)` (No extra space used other than some variables)

### Dry Run:

#### Input:
- `a = [3, 4, 1, 9, 56, 7, 9, 12]`
- `n = 8`
- `m = 5`

#### Sorted Array:
- `a = [1, 3, 4, 7, 9, 9, 12, 56]`

#### Steps:
1. `i = 0`, `j = 4`:
   - Subset: `[1, 3, 4, 7, 9]`
   - Difference: `9 - 1 = 8`
   - `min = 8`

2. `i = 1`, `j = 5`:
   - Subset: `[3, 4, 7, 9, 9]`
   - Difference: `9 - 3 = 6`
   - `min = 6`

3. `i = 2`, `j = 6`:
   - Subset: `[4, 7, 9, 9, 12]`
   - Difference: `12 - 4 = 8`
   - `min = 6`

4. `i = 3`, `j = 7`:
   - Subset: `[7, 9, 9, 12, 56]`
   - Difference: `56 - 7 = 49`
   - `min = 6`

#### Final Minimum Difference:
- `min = 6`

### Final Code with Comments:
```java
import java.util.*;

class Solution {
    public long findMinDiff(ArrayList<Integer> a, int n, int m) {
        // Sort the array
        Collections.sort(a);

        // Initialize min with maximum integer value
        long min = Integer.MAX_VALUE;

        // Initialize j to be the end index of the first subset
        int j = m - 1;

        // Loop through the array
        for (int i = 0; j < n; i++) {
            // Calculate the difference between the maximum and minimum of the current subset
            min = Math.min(min, a.get(j) - a.get(i));
            // Move to the next subset
            j++;
        }

        // Return the minimum difference found
        return min;
    }
}
```
