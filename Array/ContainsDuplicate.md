Bilkul! Pehle hum saare approaches ko Hindi mein samajhte hain, phir main Markdown format mein convert karke deta hoon.

## Approach 1: Brute Force
### Intuition:
Har element ko array ke har doosre element ke saath compare karte hain duplicates check karne ke liye. Agar duplicate milta hai, toh true return karte hain. Simple hai, lekin iska time complexity O(n^2) hai, jo bade arrays ke liye efficient nahi hai.

### Explanation:
- Har element ko baaki elements ke saath compare karo.
- Agar duplicate milta hai, toh true return karo.
- Agar nahi milta, toh false return karo.

### Code:
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] == nums[j])
                    return true;
            }
        }
        return false;
    }
}
```

## Approach 2: Sorting
### Intuition:
Array ko sort kar lo, fir adjacent elements ko check karo. Agar duplicate milta hai, toh true return karo. Sorting karne se duplicates ek saath aa jaate hain, check karna easy ho jaata hai. Time complexity O(n log n) hoti hai.

### Explanation:
- Array ko sort karo.
- Adjacent elements ko compare karo.
- Agar duplicate milta hai, toh true return karo, nahi toh false.

### Code:
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        for (int i = 1; i < n; i++) {
            if (nums[i] == nums[i - 1])
                return true;
        }
        return false;
    }
}
```

## Approach 3: Hash Set
### Intuition:
Hash set data structure ka use karke encountered elements ko store karo. Agar element pehle se set mein hai, toh true return karo. Nahi toh element ko set mein add karo. Iska time complexity O(n) hai, jo efficient hai.

### Explanation:
- Hash set use karo.
- Array ke elements ko iterate karo.
- Agar element pehle se set mein hai, toh true return karo.
- Nahi toh element ko set mein add karo.
- Agar loop complete hota hai bina duplicates mile, toh false return karo.

### Code:
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num))
                return true;
            seen.add(num);
        }
        return false;
    }
}
```

## Approach 4: Hash Map
### Intuition:
Hash map ka use karke elements aur unke counts store karo. Agar duplicate element milta hai (count >= 1), toh true return karo. Ye approach O(n) time complexity ke saath aata hai aur zyada information provide karta hai.

### Explanation:
- Hash map use karo.
- Array ke elements ko iterate karo aur unke counts store karo.
- Agar element pehle se map mein hai aur count >= 1, toh true return karo.
- Agar loop complete hota hai bina duplicates mile, toh false return karo.

### Code:
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> seen = new HashMap<>();
        for (int num : nums) {
            if (seen.containsKey(num) && seen.get(num) >= 1)
                return true;
            seen.put(num, seen.getOrDefault(num, 0) + 1);
        }
        return false;
    }
}
```

