# 📘 Lesson 8: Stack Using Dynamic Arrays

## 💡 Why Use Dynamic Arrays for Stacks?

In the previous lesson, we used a **static, fixed-size array** to build a stack. While simple and fast, it suffers from a fatal flaw: **fixed capacity**.

### 🚫 Problems with Static Arrays:

* A small stack may **overflow quickly**
* A large stack may **waste memory**

### ✅ Enter: Dynamic Stack

With **dynamic arrays** (allocated on the heap):

* 🔁 **Flexibility**: Grows during runtime — no compile-time size limits
* 💾 **Efficiency**: Allocates only what's necessary
* ⚙️ **Implementation**:

  * In **C**: `malloc()` + `realloc()`
  * In **Python**: Lists do it *automatically*

---

## 💻 Python Implementation: Dynamic Stack Class

Python's built-in `list` already supports dynamic resizing. We wrap it in a class for a cleaner, more formal structure.

```python
class DynamicStack:
    def __init__(self):
        """Initializes an empty list to serve as the stack."""
        self.stack = []

    def push(self, value):
        """Adds an element to the top of the stack."""
        self.stack.append(value)
        print(f"Pushed: {value}")

    def pop(self):
        """Removes and returns the top element of the stack."""
        if not self.stack:
            print("Stack Underflow!")
        else:
            print(f"Popped: {self.stack.pop()}")

    def peek(self):
        """Returns the top element without removing it."""
        if not self.stack:
            print("Stack is Empty")
        else:
            print(f"Top: {self.stack[-1]}")

    def traverse(self):
        """Displays the stack elements from top to bottom."""
        if not self.stack:
            print("Stack is Empty")
        else:
            print("Stack (Top to Bottom):", self.stack[::-1])

# --- Test Cases ---
ds = DynamicStack()
ds.push(10)
ds.push(20)
ds.peek()
ds.traverse()
ds.pop()
ds.traverse()
```

### 🧩 Line-by-Line Insight

* `class DynamicStack:` → Defines the stack blueprint
* `self.stack = []` → Initializes with an empty list
* `append()` → Python handles dynamic resizing internally
* `[::-1]` → Displays stack top to bottom (reverse order)

---

## 💻 C Implementation: Manual Dynamic Stack

Unlike Python, in C you must manage memory yourself.

```c
#include <stdio.h>
#include <stdlib.h> // For malloc, realloc, free

int *stack;
int top = -1;
int capacity = 2;

void push(int value) {
    if (top == capacity - 1) {
        capacity *= 2;
        stack = realloc(stack, capacity * sizeof(int));
        if (stack == NULL) {
            printf("Memory reallocation failed!\n");
            return;
        }
        printf("Resized stack to capacity %d\n", capacity);
    }
    stack[++top] = value;
    printf("Pushed: %d\n", value);
}

void pop() {
    if (top == -1) {
        printf("Stack Underflow!\n");
    } else {
        printf("Popped: %d\n", stack[top--]);
    }
}

void peek() {
    if (top == -1) {
        printf("Stack is Empty\n");
    } else {
        printf("Top: %d\n", stack[top]);
    }
}

void traverse() {
    if (top == -1) {
        printf("Stack is Empty\n");
    } else {
        printf("Stack (Top to Bottom): ");
        for (int i = top; i >= 0; i--)
            printf("%d ", stack[i]);
        printf("\n");
    }
}

int main() {
    stack = malloc(capacity * sizeof(int));

    push(10);
    push(20);
    push(30); // Triggers resize
    peek();
    traverse();
    pop();
    traverse();

    free(stack); // Always free heap memory
    return 0;
}
```

### 🧩 Line-by-Line Insight

* `int *stack;` → Pointer to dynamically allocated array
* `capacity = 2;` → Initial size
* `realloc(...)` → Doubles the capacity
* `free(stack);` → Essential to avoid memory leaks

---

## ✅ Summary

| Feature            | Static Stack       | Dynamic Stack         |
| ------------------ | ------------------ | --------------------- |
| Size               | Fixed at compile   | Grows at runtime      |
| Overflow Handling  | Manual/Not allowed | Automatically resizes |
| Memory Utilization | Can be wasteful    | More efficient        |

* **Python**: Dynamic stack via built-in `list`
* **C**: Manual implementation with `malloc()`, `realloc()`, `free()`
* **Key**: Resize stack when `top == capacity - 1`

---

## 📘 Viva Questions & Answers

**Q1: Why use dynamic arrays for stacks?**
🟢 To eliminate fixed size limitations and reduce memory waste by resizing as needed.

**Q2: What is `realloc()`? How is it different from `malloc()`?**
🟢 `malloc()` → Allocates new memory.
🟢 `realloc()` → Resizes previously allocated memory block.

**Q3: How is resizing handled?**
🟢 When full, double the `capacity` and call `realloc()` to expand.

**Q4: What’s the time complexity of push with resizing?**
🟢 Normal `push()` → O(1)
🟢 Resizing `push()` → O(n)
🟢 **Amortized time**: O(1)

---

## ⏭️ Next Up:

📘 **Lesson 9: Applications of Stacks**
➡️ Polish Notation, Infix to Postfix, and more...

---


