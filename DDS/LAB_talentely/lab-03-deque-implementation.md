# 🔢Postfix Expression Evaluation Using Stack



## 📝 What is Postfix Notation?

Postfix notation (also known as **Reverse Polish Notation - RPN**) is a mathematical notation where **operators follow their operands**.

🔹 **Infix:** `3 + 4`
🔹 **Postfix:** `3 4 +`

### ✅ Key Features:

* **No Parentheses Required** → Order of execution is unambiguous.
* **Operators Always Follow Operands** → Easy for computers to parse.
* **Perfect for Stack Evaluation** → Naturally suits LIFO operations.

📌 **Examples:**

* `(5 + 3) * (6 / 2)` → Postfix: `5 3 + 6 2 / *`
* `A + B * C` → Postfix: `A B C * +`

---

## ⚡ Why Evaluate Postfix?

Unlike infix, postfix avoids **operator precedence rules** and **parentheses matching**.

✔ **No PEMDAS needed** – order is already encoded.
✔ **Single left-to-right scan** → very efficient.
✔ **Compiler-friendly** → simplifies expression parsing.

This makes postfix evaluation **fast, predictable, and stack-based**.

---

## 🧮 The Stack-Based Algorithm

The core idea: **use a stack to store operands** until an operator arrives.

### Step-by-Step Logic:

1. **Initialize** an empty stack.
2. **Scan** each character from left to right.
3. **If operand → push onto stack.**
4. **If operator → pop two operands (`b`, `a`), compute `a operator b`, push result.**

   * ⚠️ Order matters: `a - b`, not `b - a`.
5. **Final stack value = result.**

📌 **Why stack works?**
Because it follows **LIFO** → last numbers pushed are the first needed for an operation.

---

## 💻 C++ Implementation

```cpp
#include <iostream>
#include <stack>
#include <cctype> // for isdigit()
using namespace std;

int evaluate_postfix(string expr) {
    stack<int> st; // Create a stack to store integers (operands)

    for (char ch : expr) { // Loop through each character in the string
        if (isdigit(ch)) { // 1. Check if it's a digit (0-9)
            // Convert the character to its integer value and push it
            st.push(ch - '0'); // '5' - '0' = 5 (integer)
        } else { // 2. It's an operator
            // Pop the top two operands from the stack.
            // IMPORTANT: The first pop gives the RIGHT operand (b).
            // The second pop gives the LEFT operand (a).
            int b = st.top(); st.pop();
            int a = st.top(); st.pop();

            // Perform the operation based on the operator
            switch (ch) {
                case '+': st.push(a + b); break;
                case '-': st.push(a - b); break; // a - b (order matters!)
                case '*': st.push(a * b); break;
                case '/': st.push(a / b); break; // a / b (order matters!)
                // Note: This code uses integer division.
            }
        }
    }
    // The final result is the only element left in the stack.
    return st.top();
}

int main() {
    string expr = "53+62/*";
    cout << "Postfix Expression: " << expr << endl;
    cout << "Evaluated Result  : " << evaluate_postfix(expr) << endl; // Output: 24
    return 0;
}
```

🔑 **Key Notes:**

* `ch - '0'` → ASCII trick to convert digit char → int.
* Integer division (`/`) truncates decimals.
* Correct operand order (`a op b`).

---

## 🐍 Python Implementation

```python
def evaluate_postfix(expression):
    stack = [] # Initialize an empty list to use as a stack

    for char in expression:
        if char.isdigit(): # 1. If it's a digit...
            stack.append(int(char)) # Convert to int and push
        else: # 2. If it's an operator...
            b = stack.pop() # Pop the right operand first
            a = stack.pop() # Then pop the left operand
            # Perform the operation and push the result
            if char == '+':
                stack.append(a + b)
            elif char == '-':
                stack.append(a - b) # Order: a - b
            elif char == '*':
                stack.append(a * b)
            elif char == '/':
                stack.append(a // b) # Integer division in Python is //

    return stack.pop() # Return the final result

# Test
expr = "53+62/*"
print("Postfix Expression:", expr)
print("Evaluated Result:", evaluate_postfix(expr)) # Output: 24
```

---

## 🔍 Dry Run: Evaluating `53+62/*`

Expression represents `(5 + 3) * (6 / 2)`

| Input   | Action            | Stack    | Explanation |
| ------- | ----------------- | -------- | ----------- |
| `5`     | Push 5            | \[5]     | Operand     |
| `3`     | Push 3            | \[5,3]   | Operand     |
| `+`     | Pop 3,5 → Push 8  | \[8]     | 5+3         |
| `6`     | Push 6            | \[8,6]   | Operand     |
| `2`     | Push 2            | \[8,6,2] | Operand     |
| `/`     | Pop 2,6 → Push 3  | \[8,3]   | 6/2         |
| `*`     | Pop 3,8 → Push 24 | \[24]    | 8\*3        |
| **End** | Result = 24       | \[24]    | Final       |

---

## ⏱️ Time Complexity Analysis

| Operation         | Complexity | Reason                        |
| ----------------- | ---------- | ----------------------------- |
| Overall Algorithm | **O(n)**   | Single pass through `n` chars |
| Push              | O(1)       | Constant-time stack push      |
| Pop               | O(1)       | Constant-time stack pop       |
| Digit Check       | O(1)       | Constant-time                 |

---

## ❌ Error Handling & Edge Cases

A robust implementation must check:

* **Invalid characters** (`@`, `#`) → error.
* **Too many operands** (`53 4+`) → stack not empty at end.
* **Too few operands** (`5+`) → stack underflow.
* **Division by zero** (`50/`) → error.
* **Empty input** → invalid expression.

---

## ✅ Conclusion & Real-World Applications

Mastering postfix evaluation is essential in:

* **Compilers & Interpreters** → expressions converted to postfix internally.
* **RPN Calculators** → efficient and less error-prone.
* **Virtual Machines (JVM, CLR)** → stack-based execution.
* **DSLs & Query Engines** → parsing and evaluating expressions.

📌 **Takeaway:** Postfix evaluation beautifully shows how **the right data structure (stack)** simplifies complex problems.

