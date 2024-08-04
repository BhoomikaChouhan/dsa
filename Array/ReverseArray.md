Bilkul, chalo ab hum array ko reverse karne ke alag-alag approaches ko colloquial Hindi mein samajhte hain. Har approach ko point-wise aur short mein discuss karenge.

### 1. Extra Array Use Karke (Non In-place):
- **Idea**: Ek nayi array banate hain aur original array ke elements ko reverse order mein copy karte hain.
- **Implementation**:
  - Ek nayi array `reversedArr` banate hain jo original array ke size ka hota hai.
  - Original array ke elements ko last se pehle tak copy karte hain.
  - Print karte hain reversed array.
- **Code**:
    ```java
    public class ReverseArrayExtraArray {
        public static void reverseArrayExtraArray(int[] arr) {
            int[] reversedArr = new int[arr.length];
            for (int i = 0; i < arr.length; i++) {
                reversedArr[i] = arr[arr.length - i - 1];
            }

            System.out.print("Reversed Array: ");
            for (int i : reversedArr) {
                System.out.print(i + " ");
            }
        }

        public static void main(String[] args) {
            int[] originalArr = {1, 2, 3, 4, 5};
            reverseArrayExtraArray(originalArr);
        }
    }
    ```
- **Complexity**:
  - Time: O(n)
  - Space: O(n)

### 2. Loop Use Karke (In-place):
- **Idea**: Do pointers (start aur end) use karte hain aur elements ko swap karte hain jab tak start end se chhota rahe.
- **Implementation**:
  - Start aur end indices set karte hain.
  - Start aur end elements ko swap karte hain, phir pointers ko adjust karte hain.
- **Code**:
    ```java
    public class GFG {
        static void reverseArray(int arr[], int start, int end) {
            int temp;
            while (start < end) {
                temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                start++;
                end--;
            }
        }

        static void printArray(int arr[], int size) {
            for (int i = 0; i < size; i++)
                System.out.print(arr[i] + " ");
            System.out.println();
        }

        public static void main(String args[]) {
            int arr[] = {1, 2, 3, 4, 5, 6};
            printArray(arr, 6);
            reverseArray(arr, 0, 5);
            System.out.print("Reversed array is \n");
            printArray(arr, 6);
        }
    }
    ```
- **Complexity**:
  - Time: O(n)
  - Space: O(1)

### 3. Inbuilt Methods (Non In-place):
- **Idea**: Inbuilt methods ka use karte hain, jaise Python mein `reverse()` ya Java mein array ko manually reverse karte hain.
- **Implementation**:
  - Original array ke elements ko reverse order mein copy karte hain nayi array mein.
  - Print karte hain reversed array.
- **Code**:
    ```java
    import java.util.Arrays;

    public class ArrayReverse {
        public static void main(String[] args) {
            int[] originalArray = {1, 2, 3, 4, 5};

            int[] reversedArray = new int[originalArray.length];
            for (int i = 0; i < originalArray.length; i++) {
                reversedArray[i] = originalArray[originalArray.length - 1 - i];
            }

            System.out.println(Arrays.toString(reversedArray));
        }
    }
    ```
- **Complexity**:
  - Time: O(n)
  - Space: O(1) (In-place methods ke liye)

### 4. Recursion (In-place ya Non In-place):
- **Idea**: Recursive function banate hain jo array ke first aur last elements ko swap kare aur baaki array ko recursively reverse kare.
- **Implementation**:
  - Base case: Agar start end se bada ya barabar ho jaye.
  - Swap karte hain start aur end elements ko, phir function ko recursively call karte hain baaki array ke liye.
- **Code**:
    ```java
    public class ReverseArray {
        static void reverseArray(int arr[], int start, int end) {
            int temp;
            if (start >= end)
                return;
            temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            reverseArray(arr, start + 1, end - 1);
        }

        static void printArray(int arr[], int size) {
            for (int i = 0; i < size; i++)
                System.out.print(arr[i] + " ");
            System.out.println();
        }

        public static void main(String[] args) {
            int arr[] = {1, 2, 3, 4, 5, 6};
            printArray(arr, 6);
            reverseArray(arr, 0, 5);
            System.out.println("Reversed array is ");
            printArray(arr, 6);
        }
    }
    ```
- **Complexity**:
  - Time: O(n)
  - Space: O(n) for non in-place, O(log n) for in-place (due to recursion stack)

### 5. Stack Use Karke (Non In-place):
- **Idea**: Array ke elements ko stack mein push karte hain aur phir stack se pop karke reversed array banate hain.
- **Implementation**:
  - Stack banate hain aur array ke saare elements ko push karte hain.
  - Stack se elements pop karke original array mein copy karte hain.
- **Code**:
    ```java
    import java.util.Stack;

    public class ReverseArrayUsingStack {
        public static void reverseArrayUsingStack(int[] arr) {
            Stack<Integer> stack = new Stack<>();

            for (int element : arr) {
                stack.push(element);
            }

            for (int i = 0; i < arr.length; i++) {
                arr[i] = stack.pop();
            }
        }

        public static void main(String[] args) {
            int[] arr = {1, 2, 3, 4, 5};
            reverseArrayUsingStack(arr);

            System.out.print("Reversed Array: ");
            for (int element : arr) {
                System.out.print(element + " ");
            }
        }
    }
    ```
- **Complexity**:
  - Time: O(n)
  - Space: O(n)

Umeed hai ab tumhe array reverse karne ke alag-alag approaches clear ho gaye honge! Agar koi doubt ho, toh zarur puchho!
