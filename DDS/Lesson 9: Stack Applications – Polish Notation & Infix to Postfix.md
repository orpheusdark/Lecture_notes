# 📘 Lesson 9: Stack Applications – Polish Notation & Infix to Postfix

## 📌 What is Polish Notation?

**Polish Notation**, named after logician **Jan Łukasiewicz**, rewrites expressions to eliminate the need for parentheses and precedence rules — perfect for computer parsing via stacks.

### 🧾 Types of Polish Notation

| Type        | Example | Description                                            |
| ----------- | ------- | ------------------------------------------------------ |
| Infix       | `A + B` | Human-readable, needs precedence/parentheses           |
| **Postfix** | `A B +` | Operator after operands — unambiguous & stack-friendly |
| Prefix      | `+ A B` | Operator before operands — used in compilers           |

> 🔍 This lesson focuses on **Infix ➡️ Postfix** — a key transformation for evaluation.

---

## 🤔 Why is Postfix Useful?

* ✅ **No need for parentheses**
* ✅ **No ambiguity in precedence**
* ✅ **Easy stack-based evaluation**
* ✅ Used by calculators, interpreters, and compilers

---

## 🧠 Infix-to-Postfix Conversion Algorithm

The algorithm uses a **stack** to manage operators and parentheses:

1. 🔍 Scan the infix expression **left to right**.
2. 🧮 If it's an **operand** (letter/number), **append** to output.
3. 🧷 If it's `'('`, **push** onto stack.
4. 🎯 If it's `')'`, **pop until `'('`** is found.
5. ➕ If it's an **operator**:

   * While the top of the stack has **higher or equal precedence**, pop to output.
   * Then **push** the current operator.
6. 🏁 After scanning, **pop all remaining operators** from the stack.

---

## 💻 Python Implementation

```python
def precedence(op):
    """Returns precedence level of operator."""
    if op in ('+', '-'):
        return 1
    elif op in ('*', '/'):
        return 2
    return 0

def infix_to_postfix(expression):
    """Converts infix to postfix notation."""
    result = ""
    stack = []

    for char in expression:
        if char.isalnum():
            result += char
        elif char == '(':
            stack.append(char)
        elif char == ')':
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.pop()  # Remove '('
        else:  # Operator
            while stack and precedence(stack[-1]) >= precedence(char):
                result += stack.pop()
            stack.append(char)

    while stack:
        result += stack.pop()

    return result

# --- Test Case ---
expr = "A+B*(C-D)/E"
print("Infix  :", expr)
print("Postfix:", infix_to_postfix(expr))  # Output: ABCD-*E/+
```

### 🔍 Key Concepts

* `precedence()` handles operator hierarchy
* Stack ensures correct evaluation order
* Output is built directly in the result string

---

## 💻 C Implementation

```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define SIZE 100

char stack[SIZE];
int top = -1;

void push(char ch) {
    if (top < SIZE - 1)
        stack[++top] = ch;
}

char pop() {
    if (top != -1)
        return stack[top--];
    return '\0';
}

char peek() {
    return stack[top];
}

int precedence(char op) {
    if (op == '+' || op == '-') return 1;
    if (op == '*' || op == '/') return 2;
    return 0;
}

void infix_to_postfix(char* exp) {
    char result[SIZE];
    int k = 0;

    for (int i = 0; exp[i] != '\0'; i++) {
        char ch = exp[i];

        if (isalnum(ch)) {
            result[k++] = ch;
        } else if (ch == '(') {
            push(ch);
        } else if (ch == ')') {
            while (top != -1 && peek() != '(')
                result[k++] = pop();
            pop(); // Discard '('
        } else {
            while (top != -1 && precedence(peek()) >= precedence(ch))
                result[k++] = pop();
            push(ch);
        }
    }

    while (top != -1)
        result[k++] = pop();

    result[k] = '\0'; // Null-terminate
    printf("Postfix: %s\n", result);
}

int main() {
    char expr[] = "A+B*(C-D)/E";
    printf("Infix: %s\n", expr);
    infix_to_postfix(expr);
    return 0;
}
```

### 🔍 Breakdown

* `isalnum()` → checks if char is operand
* `push()/pop()` → core stack operations
* `precedence()` → manages operator hierarchy
* Final result is stored in `result[]` and null-terminated

---

## ✅ Summary

| Concept              | Insight                                                 |
| -------------------- | ------------------------------------------------------- |
| Postfix Notation     | Simplifies evaluation — no parentheses, no ambiguity    |
| Stack Role           | Stores operators, ensures correct order and precedence  |
| Conversion Algorithm | Scans left to right, appends operands, stacks operators |
| Python               | Simplified with dynamic lists                           |
| C                    | Manual stack with arrays and indexing                   |

---

## 📘 Viva Questions & Answers

### ❓ What is Polish Notation?

📌 A system where operators are placed before (Prefix) or after (Postfix) operands — **removes the need for parentheses**.

---

### ❓ Why is Postfix better for evaluation?

📌 It's **unambiguous**, evaluated in **one left-to-right pass**, and perfectly suited for **stack-based computation**.

---

### ❓ What is the stack's role in the conversion?

📌 It **temporarily stores operators and parentheses**, ensuring they are applied in correct order when popped.

---

### ❓ How is operator precedence handled?

📌 When an operator is encountered:

* It's compared with the top of the stack.
* If the stack’s top operator has **higher or equal precedence**, it’s popped and added to the output.
* Then the current operator is **pushed**.

---

## ⏭️ Next Up

📘 **Lesson 10: Evaluation of Postfix Expressions**
👉 Dive deeper into how postfix expressions are computed using a stack at runtime.

---


