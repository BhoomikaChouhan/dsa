### Question: Minimum Sum of Absolute Differences of Pairs

**Difficulty**: Easy  
**Accuracy**: 77.05%  
**Points**: 2  

You are given two arrays **A** and **B** of equal length **N**. Your task is to pair each element of array **A** to an element in array **B**, such that the sum of the absolute differences of all the pairs is minimum.

---

### Example 1:

**Input**:
```
N = 4  
A = {4,1,8,7}  
B = {2,3,6,5}
```

**Output**:  
```
6
```

**Explanation**:  
If we take the pairings as (1, 2), (4, 3), (7, 5), and (8, 6), the sum will be:

```
|1 - 2| + |4 - 3| + |7 - 5| + |8 - 6| = 1 + 1 + 2 + 2 = 6
```

It can be shown that this is the minimum sum we can get.

---

### Example 2:

**Input**:
```
N = 3  
A = {4,1,2}  
B = {2,4,1}
```

**Output**:
```
0
```

**Explanation**:  
If we take the pairings as (4, 4), (1, 1), and (2, 2), the sum will be:

```
|4 - 4| + |1 - 1| + |2 - 2| = 0 + 0 + 0 = 0
```

It can be shown that this is the minimum sum we can get.

---

### Your Task:

You don't need to read input or print anything. Your task is to complete the function `findMinSum()` which takes the arrays **A[]**, **B[]**, and its size **N** as inputs and returns the minimum sum of the absolute differences of the pairs.

---

### Expected Time Complexity:  
`O(N * log(N))`

### Expected Auxiliary Space:  
`O(1)`

---

### Constraints:

- `1 <= N <= 10^5`
- `0 <= A[i] <= 10^9`
- `0 <= B[i] <= 10^9`
- Sum of N over all test cases doesn't exceed `10^6`

---

### Approach:

1. **Sorting for Optimal Pairing**:  
   The idea is to sort both arrays **A** and **B** in ascending order. Once both arrays are sorted, we can pair corresponding elements together (i.e., A[i] with B[i]). This will ensure that the sum of absolute differences is minimized, because sorting ensures the smallest numbers are paired with the smallest, and the largest with the largest.

2. **Calculating Absolute Differences**:  
   After sorting, we iterate through the arrays and calculate the sum of the absolute differences for each pair. This gives us the minimum possible sum.

---

### Solution Code:

```java
class Solution { 
    long findMinSum(int[] A, int[] B, int N) {
        // Sort both arrays
        Arrays.sort(A);
        Arrays.sort(B);
        
        long ans = 0;
        
        // Calculate sum of absolute differences
        for(int i = 0; i < N; i++) {
            ans += Math.abs(A[i] - B[i]);
        }
        
        return ans;
    }
}
```

### Explanation:

1. **Sorting the Arrays**:  
   We first sort both arrays **A** and **B** in ascending order using `Arrays.sort()` which takes `O(N log N)` time.

2. **Calculating the Sum of Absolute Differences**:  
   We initialize a variable `ans` to 0, which will store the total sum. Then, we loop through the sorted arrays and add the absolute difference of corresponding elements from both arrays to `ans`.

3. **Return the Result**:  
   After the loop completes, `ans` will contain the minimum sum of absolute differences, which we return.

---

### Dry Run:

Let's dry run the solution for **Example 1**:

**Input**:
```
N = 4  
A = {4, 1, 8, 7}  
B = {2, 3, 6, 5}
```

1. **Step 1: Sorting**  
   After sorting:
   ```
   A = {1, 4, 7, 8}  
   B = {2, 3, 5, 6}
   ```

2. **Step 2: Calculate the sum of absolute differences**:
   ```
   |1 - 2| + |4 - 3| + |7 - 5| + |8 - 6|
   = 1 + 1 + 2 + 2
   = 6
   ```

**Output**:  
The minimum sum of absolute differences is `6`.

---

**Dry Run for Example 2**:

**Input**:
```
N = 3  
A = {4, 1, 2}  
B = {2, 4, 1}
```

1. **Step 1: Sorting**  
   After sorting:
   ```
   A = {1, 2, 4}  
   B = {1, 2, 4}
   ```

2. **Step 2: Calculate the sum of absolute differences**:
   ```
   |1 - 1| + |2 - 2| + |4 - 4|
   = 0 + 0 + 0
   = 0
   ```

**Output**:  
The minimum sum of absolute differences is `0`.

---

This approach guarantees the minimal sum, as sorting ensures that each element is paired optimally to minimize the absolute difference for each pair.
