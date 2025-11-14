# 🧱 Implementing a Stack Using an Array

---

## 🥞 What is a Stack? 

A **stack** is a **linear data structure** that follows a strict order for adding/removing elements.

Think of a **stack of plates** 🍽️ in a cafeteria:

* Add plate only at the **top** ➝ **Push**.
* Remove plate only from the **top** ➝ **Pop**.
* Look at the top plate without removing it ➝ **Peek**.

⚠️ You **cannot** add/remove a plate from the middle or bottom. That’s the **essence of a stack**.

✨ **Common Applications:**

* 📞 **Function Call Management** ➝ Programming uses a *call stack*.
* ↩️↪️ **Undo/Redo Operations** ➝ Text editors & design tools.
* ➗✖️ **Expression Evaluation** ➝ Compilers use stacks (e.g., infix → postfix).
* 🌐 **Browser History** ➝ Back button = stack behavior.

---

## 📥📤 LIFO Principle: Last-In, First-Out

Stack works on **LIFO (Last-In, First-Out)**.
👉 The **last element added** ➝ will be the **first removed**.

📊 **Visualization:**

```
Push(10)          [10]
Push(20)          [10, 20]
Push(30)          [10, 20, 30]  <-- Top
Pop() -> 30       [10, 20]
Pop() -> 20       [10]
Push(40)          [10, 40]
Pop() -> 40       [10]
```

---

## ⚖️ Why Use an Array?

Arrays are often used to implement stacks because:
✅ **Simplicity** ➝ Easy to understand. 👍
✅ **Cache Friendly** ➝ Contiguous memory ➝ fast CPU access ⚡.
✅ **No Pointer Overhead** ➝ Saves memory compared to linked list.

⚠️ **Main Constraint:**

* **Fixed Size!**

  * Pushing on a **full stack** ➝ **Stack Overflow** 🚫.
  * Popping from an **empty stack** ➝ **Stack Underflow** 🚫.

---

## 🛠️ Core Stack Operations

| Operation           | Description                       | Analogy                 |
| ------------------- | --------------------------------- | ----------------------- |
| **`push(value)`**   | Add element at the top.           | Add plate on top 🍽️.   |
| **`pop()`**         | Remove and return top element.    | Take top plate away.    |
| **`peek()`**        | See top element without removing. | Just look 👀.           |
| **`traverse()`**    | Display all elements.             | View stack of plates.   |
| **`search(value)`** | Find position of an element.      | Locate plate in stack.  |
| **`isEmpty()`**     | Check if stack empty.             | No plates left.         |
| **`isFull()`**      | Check if stack full.              | Stack cannot hold more. |

---

## 🧠 Logic Building: The Blueprint

To build a stack using an array, we need:

1. **`arr`** ➝ The container for elements.
2. **`capacity`** ➝ Max size.
3. **`top`** ➝ Index of top element.

👉 **Initialization:**

* Start with `top = -1` ➝ means empty.

🔹 **Push:**

1. If `top == capacity - 1` ➝ **Overflow**.
2. Else increment `top`.
3. Insert at `arr[top]`.

🔹 **Pop:**

1. If `top == -1` ➝ **Underflow**.
2. Else return `arr[top]`.
3. Decrement `top`.

---

## 💻 C++ Code Walkthrough

```cpp
#include <iostream>
using namespace std;

class Stack {
    int* arr;      // Pointer to dynamically allocate the array
    int top;       // Index of the top element
    int capacity;  // Maximum size of the stack

public:
    // Constructor: Initializes the stack with a given size
    Stack(int size) {
        capacity = size;
        arr = new int[capacity]; // Allocate memory for the array on the Heap
        top = -1;                // Initialize top to -1 (empty stack)
    }

    // Destructor: Frees the dynamically allocated memory to prevent leaks
    ~Stack() {
        delete[] arr;
    }

    // Push operation: Adds an element to the top
    void push(int value) {
        if (top == capacity - 1) { // Check for Stack Overflow
            cout << "Stack Overflow" << endl;
            return;
        }
        arr[++top] = value; // First increment top, then assign value to new top index
        cout << "Pushed: " << value << endl;
    }

    // Pop operation: Removes and returns the top element
    void pop() {
        if (top == -1) { // Check for Stack Underflow
            cout << "Stack Underflow" << endl;
            return;
        }
        cout << "Popped: " << arr[top--] << endl; // Get value at top, then decrement top
    }

    // Peek operation: Returns the top element without removing it
    void peek() {
        if (top == -1) {
            cout << "Stack is empty" << endl;
        } else {
            cout << "Top element: " << arr[top] << endl;
        }
    }

    // Traverse operation: Displays all elements from top to bottom
    void traverse() {
        if (top == -1) {
            cout << "Stack is empty" << endl;
            return;
        }
        cout << "Stack elements (Top to Bottom): ";
        // Loop from top down to 0 to show top element first
        for (int i = top; i >= 0; i--)
            cout << arr[i] << " ";
        cout << endl;
    }

    // Search operation: Finds the position of an element (from the top)
    void search(int value) {
        // Loop from top down to 0
        for (int i = top; i >= 0; i--) {
            if (arr[i] == value) {
                // Position from top is 0 for the top element.
                // The next one is at position 1, and so on.
                cout << "Found at position: " << (top - i) << " from the top" << endl;
                return;
            }
        }
        cout << "Element not found" << endl;
    }
};

int main() {
    int size;
    cout << "Enter stack size: ";
    cin >> size;

    Stack s(size); // Create a stack object of user-defined size

    // Demonstrate operations
    s.push(10);
    s.push(20);
    s.push(30);
    s.peek();      // Shows 30 (top)
    s.traverse();  // Shows 30, 20, 10
    s.search(20);  // Found at position 1 from top (0 is 30, 1 is 20)
    s.pop();       // Removes 30
    s.traverse();  // Shows 20, 10

    return 0;
}
```

---

## 🐍 Python Code Explanation

Python makes this even simpler because **list** acts as a dynamic array.

```python
stack = [] # Our stack is just a list

def push(value):
    stack.append(value) # Appending to a list is O(1) and analogous to push
    # In a fixed-size array implementation, we would check for overflow first.

def pop():
    if not stack: # Check for Stack Underflow (empty list is falsy)
        print("Stack Underflow")
    else:
        # list.pop() removes and returns the last element, which is our top!
        print("Popped:", stack.pop())

def peek():
    if not stack:
        print("Stack is Empty")
    else:
        # stack[-1] gets the last element, which is the top
        print("Top Element:", stack[-1])

def traverse():
    if not stack:
        print("Stack is Empty")
    else:
        # [::-1] is a slice that reverses the list, showing top first.
        print("Stack (Top to Bottom):", stack[::-1])

def search(value):
    if value in stack:
        # Find the index from the top. The top is at index len(stack)-1.
        # We reverse the list to simulate looking from the top down.
        reversed_stack = stack[::-1]
        # The position from the top is just the index in the reversed list.
        pos = reversed_stack.index(value)
        print(f"Found {value} at position {pos} from top")
    else:
        print(f"{value} not found in stack")

# Test the functions
push(10)
push(20)
push(30)
traverse() # Output: [30, 20, 10]
peek()     # Output: 30
search(20) # Output: Found 20 at position 1 from top
pop()      # Output: Popped: 30
traverse() # Output: [20, 10]
```

⚠️ **Note:** Python lists are **dynamic**, so no *Stack Overflow*.
To mimic fixed-size stack ➝ add check `if len(stack) >= max_size:`.

---

## ⏱️ Time & Space Complexity

| Operation          | Time | Explanation          |
| ------------------ | ---- | -------------------- |
| **push()** ➕       | O(1) | Insert at end.       |
| **pop()** ❌        | O(1) | Remove last element. |
| **peek()** 👀      | O(1) | Direct access.       |
| **traverse()** 🛤️ | O(n) | Visit all.           |
| **search()** 🔎    | O(n) | May check all.       |
| **Space** 📦       | O(n) | Linear to elements.  |

---

## 🥊 Array vs. Linked List Implementation

| Feature            | Array Stack                      | Linked List Stack         |
| ------------------ | -------------------------------- | ------------------------- |
| **Memory**         | No extra per element.            | Needs `next` pointer.     |
| **Performance**    | Faster (cache efficient).        | Slower (heap allocation). |
| **Flexibility**    | ❌ Fixed size, overflow possible. | ✅ Dynamic growth.         |
| **Implementation** | Easy.                            | More complex.             |

👉 **Verdict:**

* Use **Array** ➝ when max size is known, performance matters.
* Use **Linked List** ➝ when size is dynamic/unknown.

---

## 🎯 Conclusion

Implementing a stack with an array teaches:
✔️ **LIFO principle** 📚
✔️ Managing with **pointer `top`** 👆
✔️ Handling **Overflow/Underflow** 🚧
✔️ Trade-offs ➝ **Fixed-size (array)** vs **Dynamic (linked list)**

This knowledge applies to:

* Function calls ⚡
* Undo/Redo features ↩️↪️
* Expression evaluation ➗✖️

💡 **Keep practicing!** Try adding `isEmpty()` and `isFull()` to strengthen your skills 🔥

---
