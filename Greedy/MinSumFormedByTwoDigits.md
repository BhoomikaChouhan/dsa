## Question: Min Sum Formed by Digits

**Difficulty**: Easy  
**Accuracy**: 57.25%  
**Points**: 2  

Given an array of digits (values are from 0 to 9), find the **minimum possible sum** of two numbers formed from digits of the array. All digits of the given array must be used to form the two numbers.

Any combination of digits may be used to form the two numbers to be summed. Leading zeroes are permitted.

If forming two numbers is impossible (i.e., when `N == 0`), then the "sum" is the value of the only number that can be formed.

### Example 1:

**Input**:  
```
N = 6  
arr[] = {6, 8, 4, 5, 2, 3}
```

**Output**:  
```
604
```

**Explanation**:  
The minimum sum is formed by numbers `358` and `246`, and their sum is `604`.

---

### Example 2:

**Input**:  
```
N = 5  
arr[] = {5, 3, 0, 7, 4}
```

**Output**:  
```
82
```

**Explanation**:  
The minimum sum is formed by numbers `35` and `047`, and their sum is `82`.

---

### Your Task:

You do not need to print anything; printing is done by the driver code itself. Your task is to complete the function `minSum()` which takes the array `A[]` and its size `N` as inputs and returns the required sum.

---

### Expected Time Complexity:  
`O(N * log(N))`

### Expected Auxiliary Space:  
`O(N)`

---

### Constraints:

- `1 ≤ N ≤ 35`
- `0 ≤ A[] ≤ 9`
Chalo code ke sath step-by-step samajhte hain ki ye solution kaise kaam karta hai:

```java
class Solution {
    public static long minSum(int arr[], int n) {
        // Step 1: Priority Queue banate hain jo min-heap ka kaam karegi
        PriorityQueue<Integer> pq = new PriorityQueue<>();
    
        // Step 2: Dono numbers a aur b ko initialize karte hain
        long a = 0, b = 0;
    
        // Step 3: Array ke sabhi elements ko Priority Queue mein daalte hain
        for (int i = 0; i < n; i++) {
            pq.add(arr[i]); // smallest element hamesha top pe rahega
        }
    
        // Step 4: Alternating tarike se digits ko a aur b mein daalna hai
        while (!pq.isEmpty()) {
            // Sabse pehle a ke number ko 10 se multiply karo aur usme smallest element daalo
            a = a * 10 + pq.element(); // a ka digit banate hain
            pq.remove(); // us element ko remove karte hain
            
            // Agar queue abhi bhi non-empty hai, toh b mein agla element daalte hain
            if (!pq.isEmpty()) {
                b = b * 10 + pq.element(); // b ka digit banate hain
                pq.remove(); // is element ko bhi remove karte hain
            }
        }
    
        // Step 5: Dono numbers ka sum return kar dete hain
        return a + b;
    }
}
```

### Code ko samajhne ka tareeqa:

#### Step 1: Priority Queue banayi
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```
- Yaha `PriorityQueue` ka matlab hai ki smallest element hamesha top pe rahega. Jaise hi hum elements daalte hain, ye automatically unko ascending order mein arrange karta hai. 

#### Step 2: Variables `a` aur `b` banaye
```java
long a = 0, b = 0;
```
- Ye do numbers `a` aur `b` banaye jinke digits hum alternately daalenge.

#### Step 3: Array ke elements ko Priority Queue mein daala
```java
for (int i = 0; i < n; i++) {
    pq.add(arr[i]);
}
```
- Array ke har element ko priority queue mein daal diya. Queue ab sort ho chuki hai smallest element top pe hai.

#### Step 4: Alternating digits ko `a` aur `b` mein daala
```java
while (!pq.isEmpty()) {
    a = a * 10 + pq.element(); // a mein sabse chhoti value add ki
    pq.remove(); // value ko remove kiya
    
    if (!pq.isEmpty()) { 
        b = b * 10 + pq.element(); // ab b mein agla smallest element daala
        pq.remove(); // isko bhi queue se remove kar diya
    }
}
```
- Jab tak queue mein elements hain, hum pehle `a` mein digit daalenge, phir `b` mein. Har baar `a` ya `b` ko 10 se multiply karte hain taaki nayi digit sahi jagah par aa sake.
- **Example**:
  - Pehle `a = 0 * 10 + smallest element`, jaise hi `a` mein pehla digit gaya, `a` ban gaya.
  - Phir `b` mein agla smallest element daal diya.

#### Step 5: Final sum return kiya
```java
return a + b;
```
- `a` aur `b` ko sum karke return kar diya.

---

### Example Dry Run:

#### Input:
```
arr[] = [5, 3, 0, 7, 2, 1]
```

- **Queue ka contents**: [0, 1, 2, 3, 5, 7] (sorted order)

#### Dry Run:
1. **First iteration**:
   - `a = 0 * 10 + 0 = 0`
   - `b = 0 * 10 + 1 = 1`
2. **Second iteration**:
   - `a = 0 * 10 + 2 = 2`
   - `b = 1 * 10 + 3 = 13`
3. **Third iteration**:
   - `a = 2 * 10 + 5 = 25`
   - `b = 13 * 10 + 7 = 137`

#### Final Result:
```
a = 25
b = 137
Sum = 25 + 137 = 162
```

---

### Time Complexity:
- **Inserting elements in priority queue** takes `O(n log n)` (because inserting in a heap takes log time).
- **Processing the queue** takes `O(n)` because each element is removed once.

So, total time complexity: **O(n log n)**
