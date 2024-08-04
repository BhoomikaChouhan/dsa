#Two Sum
---

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

# Example 1:

Input: nums = [2,7,11,15], target = 9  
Output: [0,1]  
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

# Example 2:

Input: nums = [3,2,4], target = 6  
Output: [1,2]

# Example 3:

Input: nums = [3,3], target = 6  
Output: [0,1]

# Constraints:

2 <= nums.length <= 104  
-109 <= nums[i] <= 109  
-109 <= target <= 109  
Only one valid answer exists.

# Follow-up: Can you come up with an algorithm that is less than O(n^2) time complexity?

---

Bilkul! Two Sum problem ko point-wise samjhaata hoon with complexities aur dry run ke saath:

### Problem Statement:
- Array `nums` aur integer `target` diya gaya hai.
- Do aise elements find karne hain jinka sum `target` ke barabar ho.
- Un elements ke indices return karne hain.

### Approaches:

#### 1. Brute Force (O(n^2) Time Complexity):
1. **Loop through each pair**:
   - Nested loops use karte hue har possible pair check karte hain.
   - Agar kisi pair ka sum `target` ke barabar ho to unke indices return karte hain.
2. **Code**:
   ```java
   class Solution {
       public int[] twoSum(int[] nums, int target) {
           int n = nums.length;
           for (int i = 0; i < n - 1; i++) {
               for (int j = i + 1; j < n; j++) {
                   if (nums[i] + nums[j] == target) {
                       return new int[]{i, j};
                   }
               }
           }
           return new int[]{}; // No solution found
       }
   }
   ```

#### 2. Two-pass Hash Table (O(n) Time Complexity):
1. **First Pass**:
   - Array ke elements ko hash table mein store karte hain with their indices.
2. **Second Pass**:
   - Har element ke liye, uska complement (`target - nums[i]`) hash table mein check karte hain.
   - Agar complement mil jaye to indices return karte hain.
3. **Code**:
   ```java
   class Solution {
       public int[] twoSum(int[] nums, int target) {
           Map<Integer, Integer> numMap = new HashMap<>();
           int n = nums.length;

           // Build the hash table
           for (int i = 0; i < n; i++) {
               numMap.put(nums[i], i);
           }

           // Find the complement
           for (int i = 0; i < n; i++) {
               int complement = target - nums[i];
               if (numMap.containsKey(complement) && numMap.get(complement) != i) {
                   return new int[]{i, numMap.get(complement)};
               }
           }

           return new int[]{}; // No solution found
       }
   }
   ```

#### 3. One-pass Hash Table (O(n) Time Complexity):
1. **Single Pass**:
   - Array ke har element ko iterate karte hain.
   - Har element ka complement (`target - nums[i]`) hash table mein check karte hain.
   - Agar complement mil jaye to indices return karte hain.
   - Agar complement nahi milta to current element ko hash table mein store karte hain.
2. **Code**:
   ```java
   class Solution {
       public int[] twoSum(int[] nums, int target) {
           Map<Integer, Integer> numMap = new HashMap<>();
           int n = nums.length;

           for (int i = 0; i < n; i++) {
               int complement = target - nums[i];
               if (numMap.containsKey(complement)) {
                   return new int[]{numMap.get(complement), i};
               }
               numMap.put(nums[i], i);
           }

           return new int[]{}; // No solution found
       }
   }
   ```

### Dry Run:
#### Example 1:
- `nums = [2, 7, 11, 15]`, `target = 9`
- Using One-pass Hash Table:

1. **Iteration 1**:
   - `i = 0`, `nums[i] = 2`, `complement = 9 - 2 = 7`
   - `7` hash table mein nahi hai.
   - `2` ko hash table mein add karte hain: `{2: 0}`

2. **Iteration 2**:
   - `i = 1`, `nums[i] = 7`, `complement = 9 - 7 = 2`
   - `2` hash table mein hai with index `0`.
   - Return: `[0, 1]`

### Summary:
1. **Brute Force**:
   - Time Complexity: `O(n^2)`
   - Space Complexity: `O(1)`
   - Simple approach, but slow for large arrays.

2. **Two-pass Hash Table**:
   - Time Complexity: `O(n)`
   - Space Complexity: `O(n)`
   - Faster, but requires two passes through the array.

3. **One-pass Hash Table**:
   - Time Complexity: `O(n)`
   - Space Complexity: `O(n)`
   - Most efficient, single pass through the array.
