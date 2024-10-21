## Question: Minimum Number of Coins

**Difficulty**: Easy  
**Accuracy**: 51.25%  
**Points**: 2  

Given an infinite supply of each denomination of Indian currency `{ 1, 2, 5, 10, 20, 50, 100, 200, 500, 2000 }` and a target value `N`.  
You have to find the **minimum number of coins and/or notes** needed to make the change for `Rs N`. You must return a list containing the value of coins and notes required.

### Example 1:
**Input**:  
`N = 43`  
**Output**:  
`20 20 2 1`  
**Explanation**:  
Minimum number of coins and notes needed to make 43.

### Example 2:
**Input**:  
`N = 1000`  
**Output**:  
`500 500`  
**Explanation**:  
Minimum possible notes are 2 notes of 500.

### Your Task:
You do not need to read input or print anything. Your task is to complete the function `minPartition()` which takes the value `N` as input parameter and returns a list of integers in decreasing order representing the denominations.

### Expected Time Complexity:  
`O(N)`

### Expected Auxiliary Space:  
`O(N)`

### Constraints:
- `1 ≤ N ≤ 10^6`

---

## Solution:

### Approach:

1. **Greedy Algorithm**:  
   - We are given a set of denominations `{1, 2, 5, 10, 20, 50, 100, 200, 500, 2000}` and we want to minimize the number of coins or notes used to reach a target `N`.
   - The idea is to always pick the largest possible denomination that is less than or equal to `N`, subtract it from `N`, and repeat until `N` becomes zero.
   
2. **Steps**:
   - We start with the largest denomination (2000) and check if it can be used. If it can, we subtract it from `N` and add it to our result list.
   - We keep repeating the process with the remaining value of `N`, trying the next largest denomination if the current one is too large.
   - Continue this process until the value of `N` becomes zero.

### Code:

```java
class Solution {
    static List<Integer> minPartition(int N) {
        // Step 1: Create a list to store the answer
        List<Integer> ans = new ArrayList<>();
        
        // Step 2: Define the denominations array in Indian currency
        int a[] = {1, 2, 5, 10, 20, 50, 100, 200, 500, 2000};
        
        // Step 3: Start from the largest denomination (index 9)
        int i = a.length - 1;
        
        // Step 4: Loop until N becomes zero
        while (N != 0) {
            // Check if the current denomination is less than or equal to N
            if (a[i] <= N) {
                // Step 5: Add the denomination to the result list
                ans.add(a[i]);
                // Subtract the denomination from N
                N = N - a[i];
            } else {
                // Move to the next smaller denomination
                i--;
            }
        }
        
        // Step 6: Return the answer list
        return ans;
    }
}
```

---

### Explanation of the Code:

1. **Initial Setup**:
   - `List<Integer> ans = new ArrayList<>()`: This list will store the result, i.e., the denominations used to make the amount `N`.
   - `int a[] = {1, 2, 5, 10, 20, 50, 100, 200, 500, 2000}`: This is the array of available denominations in Indian currency, sorted in increasing order.

2. **Loop Logic**:
   - We initialize `i` as `a.length - 1` which points to the largest denomination (2000).
   - In the `while (N != 0)` loop, we check if the current denomination `a[i]` is less than or equal to `N`. If it is, we add it to the result (`ans.add(a[i])`) and subtract it from `N`.
   - If the current denomination is greater than `N`, we move to the next smaller denomination (`i--`).
   - This process continues until `N` becomes 0.

3. **Return the Result**:
   - Finally, after the loop completes, we return the `ans` list which contains the denominations that sum up to `N`.

---

### Dry Run:

Let’s dry run the code for the first example:

#### Input:
```
N = 43
```

#### Dry Run:
1. **Step 1**: Start with the largest denomination `2000`. Since `2000 > 43`, move to the next denomination.
2. **Step 2**: Similarly, skip `500`, `200`, `100`, and `50` because they are all larger than `43`.
3. **Step 3**: Now `20 <= 43`, so add `20` to the result list and subtract `20` from `43`. Now `N = 23`.
4. **Step 4**: Again `20 <= 23`, so add `20` to the result list and subtract `20` from `23`. Now `N = 3`.
5. **Step 5**: Now `2 <= 3`, so add `2` to the result list and subtract `2` from `3`. Now `N = 1`.
6. **Step 6**: Finally, `1 <= 1`, so add `1` to the result list and subtract `1` from `N`. Now `N = 0`.

#### Output:
```
Result List: [20, 20, 2, 1]
```

This is the minimum number of coins and notes needed to make `43`.

#### Final Output:
```
20 20 2 1
```

---

### Example 2 Dry Run:

#### Input:
```
N = 1000
```

#### Dry Run:
1. **Step 1**: Start with the largest denomination `2000`. Since `2000 > 1000`, move to the next denomination.
2. **Step 2**: `500 <= 1000`, so add `500` to the result list and subtract `500` from `1000`. Now `N = 500`.
3. **Step 3**: Again `500 <= 500`, so add `500` to the result list and subtract `500` from `500`. Now `N = 0`.

#### Output:
```
Result List: [500, 500]
```

#### Final Output:
```
500 500
```

---

### Time Complexity:
- The time complexity is `O(N)`, but in practice, since we are dealing with only a few denominations, the number of iterations is very small and can be considered constant time `O(1)`.

### Auxiliary Space:
- The space complexity is `O(N)` due to the space used by the `List<Integer> ans` to store the result.

---

This approach ensures that we use the minimum number of coins and notes by always picking the largest possible denomination.
