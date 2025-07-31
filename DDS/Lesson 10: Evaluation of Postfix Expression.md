
---

# 📘 Lesson 10: Evaluation of Postfix Expression

---

## 🎯 Objectives

* 🧠 Evaluate **Postfix (Reverse Polish)** expressions using a stack
* 🧮 Understand the step-by-step **evaluation algorithm**
* 💻 Implement in both **Python** and **C**
* 🌍 Discover how this ties into real-world compilers and calculators

---

## 🧠 What is a Postfix Expression?

A **postfix expression** (also called **Reverse Polish Notation** or **RPN**) places the **operator after** its **operands**.

### 🔁 Example

Infix:
`(5 + 3) * (6 / 2)`

Postfix:
`53+62/*`

---

## ❓ Why Use Postfix?

| Advantage            | Description                                                        |
| -------------------- | ------------------------------------------------------------------ |
| 🔒 Unambiguous       | No parentheses needed; order is 100% clear                         |
| ⚡ Efficient          | Evaluated **left to right** using a simple **stack**               |
| 🛠 Compiler-Friendly | Used in interpreters, calculators, compilers, and virtual machines |

---

## 💡 Postfix Evaluation Algorithm

### 🔧 Core Logic

1. 📦 **Initialize** an empty stack.
2. 🔍 **Scan** the expression left to right.
3. If the character is:

   * ✅ **Operand (digit)** → Convert to integer, **push** to stack.
   * ➕ \**Operator (+, -, *, /)** →
     a. **Pop** two operands from stack (first `b`, then `a`)
     b. Compute `a op b`
     c. **Push** the result back
4. ✅ Final result = the **last item left on the stack**

---

## 🧪 Step-by-Step Walkthrough

Expression: `53+62/*`

| Character | Action                           | Stack (Bottom → Top) |
| --------- | -------------------------------- | -------------------- |
| `5`       | Push 5                           | \[5]                 |
| `3`       | Push 3                           | \[5, 3]              |
| `+`       | Pop 3, 5 → 5 + 3 = 8 → Push 8    | \[8]                 |
| `6`       | Push 6                           | \[8, 6]              |
| `2`       | Push 2                           | \[8, 6, 2]           |
| `/`       | Pop 2, 6 → 6 / 2 = 3 → Push 3    | \[8, 3]              |
| `*`       | Pop 3, 8 → 8 \* 3 = 24 → Push 24 | \[24]                |
| **End**   | Final result = 24                | \[]                  |

---

## 💻 Python Implementation

```python
def evaluate_postfix(expression):
    stack = []

    for char in expression:
        if char.isdigit():
            stack.append(int(char))
        else:
            b = stack.pop()
            a = stack.pop()
            if char == '+':
                stack.append(a + b)
            elif char == '-':
                stack.append(a - b)
            elif char == '*':
                stack.append(a * b)
            elif char == '/':
                stack.append(a // b)  # Integer division

    return stack.pop()

# --- Test Case ---
expr = "53+62/*"
print("Postfix Expression:", expr)
print("Evaluated Result:", evaluate_postfix(expr))  # Output: 24
```

### 🔍 Breakdown

* `isdigit()` → Check for operands (digits)
* `stack.pop()` → Get operands in the correct order
* `a op b` → Perform operation then push result
* Final result: **only one value remains on stack**

---

## 💻 C Implementation

```c
#include <stdio.h>
#include <ctype.h>

#define SIZE 100

int stack[SIZE];
int top = -1;

void push(int val) {
    stack[++top] = val;
}

int pop() {
    return stack[top--];
}

int evaluate_postfix(char *exp) {
    int a, b;
    for (int i = 0; exp[i] != '\0'; i++) {
        char ch = exp[i];

        if (isdigit(ch)) {
            push(ch - '0');  // Convert char to int
        } else {
            b = pop();
            a = pop();
            switch (ch) {
                case '+': push(a + b); break;
                case '-': push(a - b); break;
                case '*': push(a * b); break;
                case '/': push(a / b); break;
            }
        }
    }
    return pop();  // Final result
}

int main() {
    char expr[] = "53+62/*";
    printf("Postfix Expression: %s\n", expr);
    printf("Evaluated Result: %d\n", evaluate_postfix(expr));  // Output: 24
    return 0;
}
```

### 🔍 Breakdown

* `ch - '0'` → Convert char digit to int
* `push()` and `pop()` → Stack management
* `switch()` handles operator logic cleanly
* Final result returned from top of stack

---

## ✅ Summary

| Concept                  | Description                                                         |
| ------------------------ | ------------------------------------------------------------------- |
| 🔢 Operand               | Pushed directly to stack                                            |
| ➕ Operator               | Pops 2 operands, performs op, pushes result                         |
| 🧠 Stack Behavior        | LIFO — Last-In-First-Out ensures correct operand order              |
| ⚙️ Evaluation Efficiency | Left-to-right, one-pass — no precedence rules or parentheses needed |

---

## 📘 Viva Questions & Answers

### ❓ Why is postfix easier to evaluate than infix?

✅ No need for parentheses or precedence rules.
✅ Can be evaluated in **one left-to-right pass** using a **stack**.

---

### ❓ How does the stack help?

✅ Temporarily stores operands.
✅ When an operator appears, the stack provides the last two operands — ready for computation.

---

### ❓ What happens when an operator is encountered?

✅ Two operands are **popped**.
✅ The operation is performed → result is **pushed** back to the stack.

---

### ❓ What if the postfix expression is invalid?

🚫 Too many **operators** → Stack underflow (not enough operands)
🚫 Too many **operands** → Stack has extra values at the end

---

## ⏭️ Next Up

📘 **Lesson 11: Recursion**
→ Dive into **Factorial**, **GCD**, **Fibonacci**, and the legendary **Tower of Hanoi**.

---


