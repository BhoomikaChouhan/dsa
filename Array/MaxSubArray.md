https://leetcode.com/problems/maximum-subarray/solutions/1595097/java-kadane-s-algorithm-explanation-using-image

### Code in Java:

```java
import java.util.*;

class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        
        int maxi = nums[0];
        int start = 0, end = 0; // final start aur end position of the maximum sum subarray
        
        int sum = 0;
        int s = 0; // temporary start position
        
        for (int i = 0; i < n; i++) {
            sum += nums[i];
            
            if (sum > maxi) {
                maxi = sum;
                start = s;
                end = i;
            }
            
            if (sum < 0) {
                sum = 0;
                s = i + 1;
            }
        }
        
        System.out.println("Maximum Sum Subarray from nums[" + start + "] = " + nums[start] + " till nums[" + end + "] = " + nums[end]);
        
        return maxi;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Sum: " + sol.maxSubArray(nums));
    }
}
```

### Explanation in Colloquial Hindi (Point-wise):

1. **Start aur end positions initialize**: 
   - `start` aur `end` variable maximum sum subarray ke starting aur ending index store karne ke liye hain.
   - `maxi` mein maximum sum store hoga.
   - `sum` temporary sum ke liye aur `s` temporary start position ke liye hai.

2. **Loop ke through sab elements traverse karo**:
   - Har element ko `sum` mein add karo.
   - Agar current `sum` `maxi` se bada hai, to `maxi` update karo aur `start` aur `end` ko current subarray ke start aur end se update karo.

3. **Negative sum ko reset karo**:
   - Agar `sum` negative ho jata hai, to `sum` ko zero kar do aur temporary start position ko next index par shift kar do.

4. **Output**:
   - Print karo maximum sum subarray ke start aur end elements.

### Time Complexity:
- **O(n)**: Ek hi baar loop chal raha hai jo array ke size `n` ke proportional hai.

### Space Complexity:
- **O(1)**: Extra space sirf kuch variables ke liye use ho raha hai, jo constant space mein aata hai.

### Dry Run:
- Array: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`
- Variables initially: `maxi = -2`, `sum = 0`, `start = 0`, `end = 0`, `s = 0`
  
1. **Iteration 1 (i = 0)**:
   - `sum = -2` (`sum + nums[0] = 0 + (-2)`)
   - `sum < 0`, to `sum = 0` aur `s = 1`
   
2. **Iteration 2 (i = 1)**:
   - `sum = 1` (`sum + nums[1] = 0 + 1`)
   - `sum > maxi`, to `maxi = 1`, `start = 1`, `end = 1`

3. **Iteration 3 (i = 2)**:
   - `sum = -2` (`sum + nums[2] = 1 + (-3)`)
   - `sum < 0`, to `sum = 0` aur `s = 3`

4. **Iteration 4 (i = 3)**:
   - `sum = 4` (`sum + nums[3] = 0 + 4`)
   - `sum > maxi`, to `maxi = 4`, `start = 3`, `end = 3`

5. **Iteration 5 (i = 4)**:
   - `sum = 3` (`sum + nums[4] = 4 + (-1)`)
   - `sum < maxi`, so no change in `maxi`

6. **Iteration 6 (i = 5)**:
   - `sum = 5` (`sum + nums[5] = 3 + 2`)
   - `sum > maxi`, to `maxi = 5`, `start = 3`, `end = 5`

7. **Iteration 7 (i = 6)**:
   - `sum = 6` (`sum + nums[6] = 5 + 1`)
   - `sum > maxi`, to `maxi = 6`, `start = 3`, `end = 6`

8. **Iteration 8 (i = 7)**:
   - `sum = 1` (`sum + nums[7] = 6 + (-5)`)
   - `sum < maxi`, so no change in `maxi`

9. **Iteration 9 (i = 8)**:
   - `sum = 5` (`sum + nums[8] = 1 + 4`)
   - `sum < maxi`, so no change in `maxi`

### Output:
- Maximum Sum Subarray from `nums[3] = 4` till `nums[6] = 1`
- Maximum Sum: `6`

Is example se aapko idea mil gaya hoga ki code kaise kaam kar raha hai aur kaise maximum sum subarray find karte hain.
