### Brute Force Approach: Sorting
#### Intuition:
- Idea yeh hai ki pehle array ko sort kar lo, fir pehla aur aakhri element return kar do.

### Step-by-Step Explanation:
1. **Sort the Array**:
   - Array ko sort karo taaki saare elements ascending order mein aa jaayein.

2. **Identify Minimum and Maximum**:
   - Sorted array ka pehla element `mn` (minimum) hota hai.
   - Sorted array ka aakhri element `mx` (maximum) hota hai.

3. **Return the Result**:
   - `mn` aur `mx` ka pair return karo.

### Code:
```java
class Solution {
    static Pair getMinMax(long a[], long n)
    {
        Arrays.sort(a);

        long mn = a[0];
        long mx = a[(int)n - 1];

        Pair ans = new Pair(mn, mx);

        return ans;
    }
}
```

### Complexity:
- **Time Complexity**: O(n log n), kyunki sorting ka time complexity O(n log n) hota hai.
- **Space Complexity**: O(1), kyunki hum constant extra space use karte hain.

### Dry Run Example:
Maan lo array `a` = [3, 5, 1, 8, 2]

1. **Sort the Array**:
   - Sorted array: [1, 2, 3, 5, 8]

2. **Identify Minimum and Maximum**:
   - `mn` = 1 (sorted array ka pehla element)
   - `mx` = 8 (sorted array ka aakhri element)

3. **Return the Result**:
   - Pair: (1, 8)

Result: Minimum element `1` aur maximum element `8` return hota hai.

Umeed hai ab tumhe brute force approach aur iska implementation samajh aa gaya hoga! Agar aur kuch poochna ho, toh zarur batana!
### Expected Approach: Minimum aur Maximum Element Dhundhna
#### Intuition:
- Idea yeh hai ki array ke har element ko iterate karte hue minimum (mn) aur maximum (mx) element ko update karte jao.

### Step-by-Step Explanation:
1. **Initialization**:
   - `mn` ko Long.MAX_VALUE se initialize karte hain (bohot bada number, taki koi bhi element isse chhota ho).
   - `mx` ko Long.MIN_VALUE se initialize karte hain (bohot chhota number, taki koi bhi element isse bada ho).

2. **Iteration**:
   - Array ke har element ko iterate karo.
   - Har step par:
     - Agar current element `mn` se chhota hai, toh `mn` ko update karo.
     - Agar current element `mx` se bada hai, toh `mx` ko update karo.

3. **Result**:
   - `mn` aur `mx` ka pair return karo, jo minimum aur maximum elements hain.

### Code:
```java
class Solution {
    public Pair<Long, Long> getMinMax(int[] arr) {
        long min = Long.MAX_VALUE;
        long max = Long.MIN_VALUE;
        for (long num : arr) {
            if (num < min) {
                min = num;
            }
            if (num > max) {
                max = num;
            }
        }
        return new Pair<>(min, max);
    }
}
```

### Complexity:
- **Time Complexity**: O(n), kyunki hum array ko ek baar iterate karte hain.
- **Space Complexity**: O(1), kyunki hum constant extra space use karte hain.

### Dry Run Example:
Maan lo array `arr` = [3, 5, 1, 8, 2]

1. **Initialization**:
   - `min` = Long.MAX_VALUE
   - `max` = Long.MIN_VALUE

2. **Iteration**:
   - Element 3:
     - `min` = 3 (kyunki 3 < Long.MAX_VALUE)
     - `max` = 3 (kyunki 3 > Long.MIN_VALUE)
   - Element 5:
     - `min` = 3 (5 < 3 nahi hai)
     - `max` = 5 (kyunki 5 > 3)
   - Element 1:
     - `min` = 1 (kyunki 1 < 3)
     - `max` = 5 (1 > 5 nahi hai)
   - Element 8:
     - `min` = 1 (8 < 1 nahi hai)
     - `max` = 8 (kyunki 8 > 5)
   - Element 2:
     - `min` = 1 (2 < 1 nahi hai)
     - `max` = 8 (2 > 8 nahi hai)

3. **Result**:
   - `min` = 1
   - `max` = 8

Result: Minimum element `1` aur maximum element `8` return hota hai.

