## Problem: Evaluate Postfix Expression

Given a string `S` representing a postfix expression, the task is to evaluate the expression and find the final value. The operators will only include the basic arithmetic operators like `*`, `/`, `+`, and `-`.

### Example 1:

**Input**:  
`S = "231*+9-"`

**Output**:  
`-4`

**Explanation**:  
After solving the given expression, we get the result as `-4`.

### Example 2:

**Input**:  
`S = "123+*8-"`

**Output**:  
`-3`

**Explanation**:  
After solving the given postfix expression, we get the result as `-3`.

### Your Task:

You do not need to read input or print anything. Complete the function `evaluatePostfixExpression()` that takes the string `S` denoting the expression as input and returns the evaluated value.

### Expected Time Complexity:
- `O(|S|)`

### Expected Auxiliary Space:
- `O(|S|)`

### Constraints:
- `1 ≤ |S| ≤ 10^5`
- `0 ≤ Si ≤ 9` (And given operators are `+`, `-`, `*`, `/`)

You need to evaluate a postfix expression where the input consists of digits (0-9) and the basic arithmetic operators (`+`, `-`, `*`, `/`). Let's break down the approach and provide the implementation in a simple and efficient way.

### Approach:
1. **Use a Stack**: Postfix expressions are evaluated using a stack. Whenever a number is encountered, it is pushed onto the stack. When an operator is encountered, the top two numbers are popped from the stack, the operation is performed, and the result is pushed back onto the stack.
2. **Operators**: The supported operators are `+`, `-`, `*`, and `/`, and the expression contains only digits and operators.
3. **Final Result**: At the end of the expression, the stack will contain the final result.

### Steps:
1. Traverse the string character by character.
2. If a character is a digit, push it onto the stack (convert from `char` to `int`).
3. If a character is an operator, pop two numbers from the stack, apply the operator, and push the result back onto the stack.
4. After processing the entire string, the result will be the only element left in the stack.

### Code Implementation:

```java
import java.util.Stack;

class Solution {
    // Function to evaluate a postfix expression.
    public static int evaluatePostfixExpression(String S) {
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < S.length(); i++) {
            char c = S.charAt(i);
            
            // If the current character is a digit, push it to the stack
            if (Character.isDigit(c)) {
                stack.push(c - '0'); // Convert char to int
            } else {
                // Pop two numbers from the stack for the operator
                int b = stack.pop();
                int a = stack.pop();
                
                // Perform the operation and push the result back onto the stack
                switch (c) {
                    case '+':
                        stack.push(a + b);
                        break;
                    case '-':
                        stack.push(a - b);
                        break;
                    case '*':
                        stack.push(a * b);
                        break;
                    case '/':
                        stack.push(a / b);
                        break;
                }
            }
        }
        
        // The final result will be the only element left in the stack
        return stack.pop();
    }
}
```

### Explanation:
1. **Digit Handling**: When a digit is encountered, it's converted from `char` to `int` by subtracting `'0'` and pushed onto the stack.
2. **Operator Handling**: For each operator (`+`, `-`, `*`, `/`), two numbers are popped from the stack, the operation is performed, and the result is pushed back onto the stack.
3. **Final Result**: At the end of the string, the stack will contain exactly one value, which is the result of the evaluated postfix expression.

### Example Walkthrough:

1. **Input 1**: `S = "231*+9-"`

   - Read `2`, push it to the stack: `stack = [2]`
   - Read `3`, push it to the stack: `stack = [2, 3]`
   - Read `1`, push it to the stack: `stack = [2, 3, 1]`
   - Read `*`, pop `1` and `3`, push `3 * 1 = 3`: `stack = [2, 3]`
   - Read `+`, pop `3` and `2`, push `2 + 3 = 5`: `stack = [5]`
   - Read `9`, push it to the stack: `stack = [5, 9]`
   - Read `-`, pop `9` and `5`, push `5 - 9 = -4`: `stack = [-4]`
   - Final result: `-4`

2. **Input 2**: `S = "123+*8-"`

   - Read `1`, push it to the stack: `stack = [1]`
   - Read `2`, push it to the stack: `stack = [1, 2]`
   - Read `3`, push it to the stack: `stack = [1, 2, 3]`
   - Read `+`, pop `3` and `2`, push `2 + 3 = 5`: `stack = [1, 5]`
   - Read `*`, pop `5` and `1`, push `1 * 5 = 5`: `stack = [5]`
   - Read `8`, push it to the stack: `stack = [5, 8]`
   - Read `-`, pop `8` and `5`, push `5 - 8 = -3`: `stack = [-3]`
   - Final result: `-3`

### Time Complexity:
- **O(|S|)**: We iterate through the string `S` once, and each stack operation (push, pop) takes constant time, so the time complexity is linear with respect to the length of the string.

### Space Complexity:
- **O(|S|)**: The space complexity is linear due to the stack, which can hold up to `|S|`/2 elements in the worst case, as half of the characters could be operands.
