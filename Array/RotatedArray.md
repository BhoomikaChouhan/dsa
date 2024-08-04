https://leetcode.com/problems/search-in-rotated-sorted-array/submissions/1340852898/

Bilkul, chalo is `Solution` class ka code detail mein samajhte hain aur dry run karte hain.

### Code Ka Mukhya Idea:

Yeh code ek rotated sorted array mein target element ko search karta hai. Yeh 2 major functions ka use karta hai:
1. **`getPivot`**: Jo array ka pivot (minimum element ka index) find karta hai.
2. **`Bs`**: Binary search function jo given range mein target element ko search karta hai.

### Step-by-Step Explanation:

#### 1. `Bs` Function (Binary Search):

```java
public int Bs(int[] a, int s, int e, int tar) {
    while (s <= e) {
        int mid = s + (e - s) / 2;

        if (a[mid] == tar) {
            return mid;
        }

        if (tar < a[mid]) {
            e = mid - 1;
        }

        if (tar > a[mid]) {
            s = mid + 1;
        }
    }
    return -1;
}
```

- Yeh function binary search algorithm implement karta hai. 
- `mid` ko calculate karta hai aur target `tar` ko `a[mid]` se compare karta hai.
- Agar target mil jata hai, `mid` return karta hai.
- Agar target `a[mid]` se chhota hai, end index `e` ko `mid - 1` set karta hai.
- Agar target `a[mid]` se bada hai, start index `s` ko `mid + 1` set karta hai.
- Agar target nahi milta, -1 return karta hai.

#### 2. `getPivot` Function:

```java
public int getPivot(int[] a) {
    int n = a.length;
    int s = 0;
    int e = n - 1;

    int mid = s + (e - s) / 2;

    while (s < e) {
        if (a[mid] >= a[0]) {
            s = mid + 1;
        } else {
            e = mid;
        }
        mid = s + (e - s) / 2;
    }

    return s;
}
```

- Yeh function rotated sorted array mein pivot element (minimum element) ka index find karta hai.
- Start `s` aur end `e` indices set karta hai aur `mid` calculate karta hai.
- Agar `a[mid]` first element `a[0]` se bada ya barabar hai, start index `s` ko `mid + 1` set karta hai.
- Warna, end index `e` ko `mid` set karta hai.
- Jab loop khatam hota hai, `s` pivot index hota hai.

#### 3. `search` Function:

```java
public int search(int[] a, int tar) {
    int n = a.length;

    int k = getPivot(a);
    int s = 0;
    int e = n - 1;

    if (tar >= a[s]) {
        return Bs(a, s, k, tar);
    }
    if (tar <= a[s]) {
        return Bs(a, k, e, tar);
    }
    return -1;
}
```

- Yeh function overall search ko handle karta hai.
- Pehle pivot index `k` ko find karta hai using `getPivot` function.
- Phir decide karta hai ki target element kaunse half mein hai:
  - Agar target `a[s]` ke barabar ya bada hai, binary search `Bs` ko left half (start se pivot tak) call karta hai.
  - Agar target `a[s]` se chhota hai, binary search `Bs` ko right half (pivot se end tak) call karta hai.
- Agar target nahi milta, -1 return karta hai.

### Time Complexity:
- **`getPivot` function**: Iski time complexity O(log n) hai kyunki yeh binary search ka use karta hai.
- **`Bs` (Binary Search) function**: Iski time complexity bhi O(log n) hai.
- **Overall `search` function**: Kyunki yeh do binary searches use karta hai (ek pivot find karne ke liye aur ek target search karne ke liye), total time complexity O(log n) hoti hai.

### Space Complexity:
- Sabhi functions constant extra space use karte hain (i.e., O(1)), kyunki yeh iterative solutions hain aur koi extra data structures use nahi karte.

Toh overall, is solution ki:
- **Time Complexity**: O(log n)
- **Space Complexity**: O(1)

---

### Simplified Summary:
1. **Time Complexity**: O(log n)
2. **Space Complexity**: O(1)

### Dry Run Example:

Maan lo `a` = [4, 5, 6, 7, 0, 1, 2] aur `tar` = 0.

1. **`getPivot` Call**:
   - `n = 7`, `s = 0`, `e = 6`
   - Initial `mid` = 3 (`a[3]` = 7)
   - Since `a[mid]` >= `a[0]`, `s = 4`
   - New `mid` = 5 (`a[5]` = 1)
   - Since `a[mid]` < `a[0]`, `e = 5`
   - New `mid` = 4 (`a[4]` = 0)
   - Since `a[mid]` < `a[0]`, `e = 4`
   - Loop ends, `s = 4`, `pivot` = 4

2. **`search` Call**:
   - `k = 4`, `s = 0`, `e = 6`
   - Since `tar` <= `a[s]` is false, call `Bs(a, k, e, tar)`:
     - `Bs(a, 4, 6, 0)`
     - `s = 4`, `e = 6`
     - Initial `mid` = 5 (`a[5]` = 1)
     - Since `tar` < `a[mid]`, `e = 4`
     - New `mid` = 4 (`a[4]` = 0)
     - `a[mid]` == `tar`, return 4

Result: `search` function returns 4, which is the index of `tar` = 0 in the array `a`.

Umeed hai ab tumhe pura code aur uska kaam samajh aa gaya hoga! Agar kuch aur doubt ho to zarur poocho!
