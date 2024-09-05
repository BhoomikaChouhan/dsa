To implement a **stack** using **two queues**, we can simulate the LIFO (Last In, First Out) behavior using only the FIFO (First In, First Out) operations of the queue.

### Approach:
We will maintain two queues (`queue1` and `queue2`) to mimic stack behavior. The core idea is that every time we perform a `push()`, we rearrange the elements in such a way that the most recently added element is always at the front of `queue1`.

#### Operations:
1. **Push**: Transfer all elements from `queue1` to `queue2`, push the new element into `queue1`, and then transfer all elements back from `queue2` to `queue1`. This ensures the last added element is always at the front of `queue1`.
2. **Pop**: Just remove and return the front element of `queue1`.
3. **Top**: Simply return the front element of `queue1`.
4. **Empty**: Return `true` if `queue1` is empty, otherwise `false`.

### Java Code Implementation:

```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {
    // Two queues
    private Queue<Integer> queue1;
    private Queue<Integer> queue2;

    // Constructor to initialize the stack
    public MyStack() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }

    // Push element x onto stack
    public void push(int x) {
        // Push x into queue2
        queue2.add(x);

        // Transfer all elements from queue1 to queue2
        while (!queue1.isEmpty()) {
            queue2.add(queue1.poll());
        }

        // Swap queue1 and queue2
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }

    // Removes the element on top of the stack and returns that element
    public int pop() {
        return queue1.poll();
    }

    // Get the top element
    public int top() {
        return queue1.peek();
    }

    // Returns whether the stack is empty
    public boolean empty() {
        return queue1.isEmpty();
    }
}
```

### Explanation:
- **push(int x)**: 
  - We add the new element `x` to `queue2`.
  - Then we transfer all elements from `queue1` to `queue2` to maintain the order.
  - Finally, we swap `queue1` and `queue2` so that `queue1` contains all the elements and the last added element is at the front.
  
- **pop()**:
  - We remove and return the front element of `queue1`, which is the last added element.

- **top()**:
  - We return the front element of `queue1` without removing it.

- **empty()**:
  - We check if `queue1` is empty or not.

### Example Walkthrough:
For the input:
```java
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
```
- `push(1)`: The stack is now `[1]`.
- `push(2)`: The stack is now `[2, 1]` (2 is at the top).
- `top()`: The top element is `2`.
- `pop()`: Remove and return `2`. The stack is now `[1]`.
- `empty()`: The stack is not empty, so return `false`.

### Time Complexity:
- **push()**: O(n) where `n` is the number of elements in the stack, as we transfer elements between queues.
- **pop()**: O(1) since we simply remove from the front of `queue1`.
- **top()**: O(1) since we just peek the front of `queue1`.
- **empty()**: O(1) since we just check if `queue1` is empty.

### Space Complexity:
- **O(n)**: We are using two queues, each capable of holding `n` elements in the worst case.

This is how you can implement a stack using two queues in Java!
