# 🧠 Infix to Postfix Conversion Using Stack


---

## ➕➖✖️➗ What are Infix, Prefix, and Postfix?

Mathematical expressions can be written in **three notations**:

* **Infix Notation (Human-friendly)** → Operator between operands
  Example: `A + B`, `3 * (5 - 2)`

* **Prefix (Polish) Notation** → Operator before operands
  Example: `+ A B`, `* 3 - 5 2`

* **Postfix (Reverse Polish) Notation** → Operator after operands
  Example: `A B +`, `3 5 2 - *`

💡 **Why do computers prefer Postfix?**
Because it eliminates **parentheses and precedence rules**, making evaluation fast and unambiguous using just a **stack**.

---

## ⚡ Why Convert to Postfix?

Take `3 + 5 * 2`.

* In **Infix**, precedence must be considered → Answer = `13`.
* In **Postfix**, it becomes `3 5 2 * +`, and evaluation is simply **left to right with a stack**.

✅ Postfix removes complexity → **no precedence rules, no parentheses, no lookahead**.

---

## 🥇 The Core Challenge: Operator Precedence

To correctly convert, we must respect operator rules:

| Operator | Precedence  | Associativity |
| -------- | ----------- | ------------- |
| `*`, `/` | 2           | Left-to-Right |
| `+`, `-` | 1           | Left-to-Right |
| `(`      | 0 (special) | -             |

📌 Key rules:

1. `*` and `/` > `+` and `-`
2. Parentheses override precedence
3. Same precedence → evaluate **left to right**

---

## 🧮 The Algorithm: Step-by-Step Logic

The conversion algorithm (scan **left → right**):

1. **Operand (letter/number):** → Add directly to output
2. **Opening `(`:** → Push to stack
3. **Closing `)`:** → Pop until `(` is found (discard `(`)
4. \**Operator (+, -, *, /):**

   * While stack not empty AND top has **higher or equal precedence**, pop and add to output
   * Then push the current operator
5. **End of expression:** → Pop all remaining operators

---

## 🧩 The Role of the Stack

Think of the **stack** as the *decision-maker*:

* **Holds operators** until it’s safe to output them
* **Maintains precedence** order automatically
* **Handles parentheses** as temporary boundaries

👉 **Analogy:**
Operands = ingredients 🍅 (go straight to the plate)
Operators = tools 🍴 (wait on the counter until needed)
Parentheses = new recipe 🥘 (finish it before returning to the main one).

---

## 💻 C++ Code 

```cpp
#include <iostream>
#include <stack>
#include <cctype> // for isalnum()
using namespace std;

// Function to determine the precedence of an operator
int precedence(char op) {
    if (op == '+' || op == '-') return 1;
    if (op == '*' || op == '/') return 2;
    return 0; // Return 0 for any other character (like '(')
}

// The main conversion function
string infix_to_postfix(string expr) {
    stack<char> st; // Stack to hold operators and '('
    string result = ""; // String to build the postfix output

    // Loop through each character in the input expression
    for (char ch : expr) {
        // 1. If it's an operand (letter or digit), add to result.
        if (isalnum(ch)) {
            result += ch;
        }
        // 2. If it's '(', push it onto the stack.
        else if (ch == '(') {
            st.push(ch);
        }
        // 3. If it's ')', pop and output until '(' is found.
        else if (ch == ')') {
            while (!st.empty() && st.top() != '(') {
                result += st.top();
                st.pop();
            }
            st.pop(); // Pop and discard the '('
        }
        // 4. If it's an operator (+, -, *, /)
        else {
            // While stack is not empty and the top operator has >= precedence...
            while (!st.empty() && precedence(st.top()) >= precedence(ch)) {
                result += st.top(); // ...pop it to the output.
                st.pop();
            }
            st.push(ch); // Then push the current operator onto the stack.
        }
    }

    // 5. Pop all remaining operators from the stack
    while (!st.empty()) {
        result += st.top();
        st.pop();
    }

    return result; // Return the final postfix string
}

int main() {
    string expr = "A+B*(C-D)/E";
    cout << "Infix   : " << expr << endl;
    cout << "Postfix : " << infix_to_postfix(expr) << endl; // Output: ABCD-*E/+
    return 0;
}
```

---

## 🐍 Python Code 

```python
def precedence(op):
    if op == '+' or op == '-':
        return 1
    elif op == '*' or op == '/':
        return 2
    return 0 # For '(' or other characters

def infix_to_postfix(expression):
    result = "" # Output string
    stack = []  # Our stack (using a list)

    for char in expression:
        if char.isalnum():  # 1. Operand
            result += char
        elif char == '(':   # 2. Open parenthesis
            stack.append(char)
        elif char == ')':   # 3. Close parenthesis
            # Pop until we find the matching '('
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.pop() # Remove the '(' from the stack
        else:               # 4. Operator
            # Check precedence of stack top vs current operator
            while stack and precedence(stack[-1]) >= precedence(char):
                result += stack.pop()
            stack.append(char) # Push the current operator

    # 5. Pop all remaining operators
    while stack:
        result += stack.pop()

    return result
```

---

## 🔍 Dry Run Example

Expression: **`A+B*(C-D)/E`**

| Input | Action                    | Stack          | Output      |
| ----- | ------------------------- | -------------- | ----------- |
| `A`   | Operand → Output          | `[]`           | `A`         |
| `+`   | Push                      | `[+]`          | `A`         |
| `B`   | Operand → Output          | `[+]`          | `AB`        |
| `*`   | Push (higher prec than +) | `[+, *]`       | `AB`        |
| `(`   | Push                      | `[+, *, (]`    | `AB`        |
| `C`   | Operand → Output          | `[+, *, (]`    | `ABC`       |
| `-`   | Push                      | `[+, *, (, -]` | `ABC`       |
| `D`   | Operand → Output          | `[+, *, (, -]` | `ABCD`      |
| `)`   | Pop until `(`             | `[+, *]`       | `ABCD-`     |
| `/`   | Pop `*`, then push `/`    | `[+, /]`       | `ABCD-*`    |
| `E`   | Operand → Output          | `[+, /]`       | `ABCD-*E`   |
| End   | Pop `/` then `+`          | `[]`           | `ABCD-*E/+` |

✅ Final Postfix: **`ABCD-*E/+`**

---

## ✅ Conclusion & Applications

* Postfix conversion is the **foundation of expression evaluation**.
* The **stack** ensures rules are applied systematically without confusion.

📌 **Applications:**

* Compilers & Interpreters → Parsing expressions
* Scientific Calculators → Internal computation
* Spreadsheet & Formula Processors → Efficient evaluation

---
