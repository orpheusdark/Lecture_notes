
---

# 📘 Lesson 7: Stack – Definition & Operations (Array Representation)

## 🔁 What is a Stack?

A **Stack** is a **linear data structure** that operates on **LIFO**:
➡️ **Last-In, First-Out**
The **last item added** is the **first to be removed**.

---

### 🧠 Real-World Analogy

Think of a stack like a **pile of plates**:
🍽️ Add plates to the **top**, and when needed, remove from the **top**.
You can't pull a plate from the bottom without removing everything above it.

---

## 🔧 Core Stack Operations (All O(1) Time Complexity)

| Operation   | Description                                          |
| ----------- | ---------------------------------------------------- |
| `push(x)`   | ➕ Adds item `x` to the top of the stack              |
| `pop()`     | ➖ Removes and returns the top item                   |
| `peek()`    | 👀 Returns the top item without removing it          |
| `isEmpty()` | ❓ Returns `true` if the stack is empty, else `false` |

---

## 💡 Real-Life Applications

* 🔙 **Undo Feature** in text editors and Photoshop
* 🌐 **Browser History** → Back button
* 📞 **Function Call Stack** in recursion and nested function calls

---

## 🧠 Stack in Memory – Array Representation

* 🗃️ Stack is stored in a fixed-size **array**
* 🧮 A variable `top` keeps track of the **last inserted element**
* 📉 Initially, `top = -1` (empty stack)

### 🔧 Operations:

* 🔼 **push(x)**:

  1. Increment `top`
  2. Assign `array[top] = x`

* 🔽 **pop()**:

  1. Access `array[top]`
  2. Decrement `top`

---

## ⚠️ Error Handling

| Error Type      | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| ❌ **Overflow**  | Trying to push when `top == MAX_SIZE - 1`                     |
| ❌ **Underflow** | Trying to pop or peek when `top == -1` (i.e., stack is empty) |

---

## 🐍 Python Implementation (Using List)

```python
stack = []

def push(val):
    stack.append(val)
    print(f"Pushed: {val}")

def pop():
    if not stack:
        print("Stack Underflow! Cannot pop from an empty stack.")
    else:
        print(f"Popped: {stack.pop()}")

def peek():
    if not stack:
        print("Stack is Empty")
    else:
        print(f"Top Element: {stack[-1]}")

def traverse():
    if not stack:
        print("Stack is Empty")
    else:
        print("Stack (Top to Bottom):", stack[::-1])

# Test
push(10)
push(20)
peek()
traverse()
pop()
traverse()
pop()
pop()  # Underflow
```

### 🧠 Key Points:

* `stack = []`: Initialize empty list
* `append(val)`: O(1) average; adds to top
* `pop()`: O(1); removes from top
* `stack[-1]`: Access top without removing
* `stack[::-1]`: Reverses list for top-to-bottom display

---

## 🇨 C Implementation (Using Fixed-Size Array)

```c
#include <stdio.h>
#define SIZE 5

int stack[SIZE];
int top = -1;

void push(int val) {
    if (top == SIZE - 1) {
        printf("Stack Overflow! Cannot push %d.\n", val);
    } else {
        stack[++top] = val;
        printf("Pushed: %d\n", val);
    }
}

void pop() {
    if (top == -1) {
        printf("Stack Underflow! Cannot pop.\n");
    } else {
        printf("Popped: %d\n", stack[top--]);
    }
}

void peek() {
    if (top == -1) {
        printf("Stack is Empty\n");
    } else {
        printf("Top Element: %d\n", stack[top]);
    }
}

void traverse() {
    if (top == -1) {
        printf("Stack is Empty\n");
    } else {
        printf("Stack (Top to Bottom): ");
        for (int i = top; i >= 0; i--) {
            printf("%d ", stack[i]);
        }
        printf("\n");
    }
}

int main() {
    push(10);
    push(20);
    peek();
    traverse();
    pop();
    traverse();
    return 0;
}
```

### 🧠 Key Points:

* `#define SIZE 5`: Defines stack capacity
* `top = -1`: Means stack is empty
* `++top`: Increments before accessing index
* `top--`: Decrements after access (removal)
* Handles **overflow** and **underflow** conditions with checks

---

## ✅ Summary

* 🌀 A **Stack** is a **LIFO** data structure
* 🧮 Core operations: `push`, `pop`, `peek` — all O(1)
* 📦 Can be implemented using arrays or dynamic structures
* ⚠️ Always handle **Overflow** and **Underflow**

---

## 📘 Viva Q\&A

> ❓ **What is a stack? How is it different from a queue?**
> 🅰️ Stack = LIFO, Queue = FIFO (First-In, First-Out)

> ❓ **What are Overflow and Underflow in stacks?**
> 🅰️ Overflow = push into a full stack
> 🅰️ Underflow = pop from an empty stack

> ❓ **How is stack represented using arrays?**
> 🅰️ Array + `top` variable; `top = -1` when empty

> ❓ **Can we dynamically resize a stack in C?**
> 🅰️ Not with static arrays. But yes with `malloc()` and `realloc()`.

---

## ⏭️ Coming Up Next:

📘 **Lesson 8: Stack using Dynamic Arrays**

---


