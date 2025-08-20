# **🚀 LAB 5:  Queue Implementation & Operations (FIFO Principle)**


## **📜 1. Introduction: The Real-World Queue**

Imagine you're waiting in line at a **ticket counter 🎟️**, a **coffee shop ☕**, or a **printer queue 🖨️**.
👉 The person who arrives **first** is the one who gets served **first**.

This is the fundamental principle of a **Queue** data structure.

🔹 In computer science, a **Queue** is a **Linear Data Structure** that follows the **FIFO (First-In-First-Out)** principle.
The element inserted **first** will be the **first one removed**.

Think of it like a **one-way street 🚗➡️**:

* Cars enter at one end
* Exit from the other

---

## **🎯 2. The Problem & The Need**

💡 Why do we need queues?
Because computers must often manage **data or tasks** in the **exact order** they were received. Without queues, it would be chaotic!

### **📌 Common Applications of Queues:**

* ⚙️ **CPU Task Scheduling** → OS uses queues to manage processes waiting for CPU.
* 🖨️ **Printer Spooling** → Print jobs line up in order.
* 🌐 **Data Buffers** → Networking & streaming use queues for packets.
* 📞 **Customer Service Systems** → Calls are queued in call centers.
* 🕸️ **Breadth-First Search (BFS)** → A core graph traversal algorithm.

👉 **The Core Challenge:** Implementing this **FIFO model** efficiently in memory while handling **limitations** (like fixed size) & providing standard operations.

---

## **🏗️ 3. Understanding the Queue Structure & Operations**

A **Queue** can be visualized as a **linear array** with **two pointers**:

* **`front`** 👉 Points to the **first element** (to be removed next).
* **`rear`** 👉 Points to the **last inserted element**.

### **🔧 Core Operations:**

1. ➡️ **`enqueue(value)`** → Add element at **rear**.
2. ⬅️ **`dequeue()`** → Remove element from **front**.
3. 👀 **`peek()` / `front()`** → Show front element *without removing*.
4. ❓ **`isEmpty()`** → Checks if queue has no elements.
5. ❓ **`isFull()`** → Checks if queue is full.
6. 📋 **`traverse()` / `display()`** → Prints all elements from `front → rear`.

---

## **🔄 4. The Critical Concept: Circular Queue**

⚠️ Problem with **Linear Queue** → **False Overflow**

Example (Queue of size 5):

1. Insert 5 → `[A, B, C, D, E]` → Full (`front=0`, `rear=4`)
2. Remove 2 → `[ , , C, D, E]` (`front=2`, `rear=4`)
3. Try adding `F` → ❌ says **Full** though space exists.

👉 **Solution: Circular Queue!** ✨
Treats array as a **circle 🔄** → When `rear` hits last index, it **wraps** back to `0` if space is free.

**Wrapping Logic using Modulo `%`:**

* `rear = (rear + 1) % SIZE`
* `front = (front + 1) % SIZE`
* Queue Full if 👉 `(rear + 1) % SIZE == front`

✅ This ensures **efficient memory use**.

---

## **🧠 5. Logic Building & Step-by-Step Examples**

Let’s trace a **Circular Queue** with `SIZE = 3`:

**Initial:** `front = -1`, `rear = -1`
👉 Queue: `[ , , ]`

### **Steps:**

1. **enqueue(10)**

   * `front=0`, `rear=0`
   * Queue: `[10, , ]`

2. **enqueue(20)**

   * `rear=1`
   * Queue: `[10, 20, ]`

3. **enqueue(30)**

   * `rear=2`
   * Queue: `[10, 20, 30]` ✅ **Full**

4. **dequeue()**

   * Removes `10`
   * Queue: `[ , 20, 30]`

5. **enqueue(40)**

   * Wraps `rear → 0`
   * Queue: `[40, 20, 30]`
   * Logical order: `20 → 30 → 40`

---

## **💻 6. Code Implementation & Explanation**

### **⚡ C++ Implementation (OOP Based)**

```cpp
#include <iostream>
#define SIZE 5 // Define the maximum size of the queue
using namespace std;

class Queue {
    int arr[SIZE]; // Array to hold queue elements
    int front, rear; // Pointers to track ends

public:
    // Constructor to initialize an empty queue
    Queue() {
        front = rear = -1; // -1 signifies the queue is empty
    }

    // Operation 1: Enqueue (Add an element to the end)
    void enqueue(int val) {
        // Check for Queue Overflow
        if ((rear + 1) % SIZE == front) {
            cout << "🚨 Queue Overflow! Can't add " << val << "." << endl;
            return;
        }
        // If the queue is empty, set front to 0
        if (front == -1) front = 0;
        // Move rear forward in a circular manner
        rear = (rear + 1) % SIZE;
        // Insert the new value at the new rear position
        arr[rear] = val;
        cout << "✅ Enqueued: " << val << endl;
    }

    // Operation 2: Dequeue (Remove an element from the front)
    void dequeue() {
        // Check for Queue Underflow
        if (front == -1) {
            cout << "🚨 Queue Underflow! Nothing to remove." << endl;
            return;
        }
        // Print the value being removed
        cout << "✅ Dequeued: " << arr[front] << endl;
        // If this was the last element, reset the queue to empty state
        if (front == rear)
            front = rear = -1;
        else // Otherwise, move front forward in a circular manner
            front = (front + 1) % SIZE;
    }

    // Operation 3: Traverse/Display (Print all elements from front to rear)
    void traverse() {
        if (front == -1) {
            cout << "📭 Queue is empty." << endl;
            return;
        }
        cout << "📋 Queue: ";
        int i = front;
        // Loop through the queue using a do-while to handle the circular nature
        while (true) {
            cout << arr[i] << " ";
            if (i == rear) break; // Stop after printing the rear element
            i = (i + 1) % SIZE; // Move to the next index circularly
        }
        cout << endl;
    }

    // Operation 4: Search (Find if an element exists in the queue)
    void search(int key) {
        if (front == -1) {
            cout << "📭 Queue is empty. Can't search." << endl;
            return;
        }
        int i = front;
        while (true) {
            if (arr[i] == key) {
                cout << "🔍 Element " << key << " found at index " << i << "." << endl;
                return;
            }
            if (i == rear) break;
            i = (i + 1) % SIZE;
        }
        cout << "🔍 Element " << key << " not found." << endl;
    }
};

int main() {
    cout << "🧪 Testing Queue Implementation (C++)" << endl;
    cout << "------------------------------------" << endl;
    Queue q; // Create a queue object

    q.traverse(); // Try to display empty queue

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50); // Queue should be full now
    q.enqueue(60); // This should cause overflow

    q.traverse();

    q.dequeue(); // Remove 10
    q.dequeue(); // Remove 20

    q.traverse(); // Should show [30, 40, 50]

    q.enqueue(60); // Should work now due to circular nature
    q.enqueue(70); // Should work

    q.traverse(); // Should show [30, 40, 50, 60, 70]

    q.search(40);
    q.search(99);

    return 0;
}
```

🧪 **Output**

```
📭 Queue is empty.
✅ Enqueued: 10
✅ Enqueued: 20
✅ Enqueued: 30
✅ Enqueued: 40
✅ Enqueued: 50
🚨 Queue Overflow! Can't add 60.
📋 Queue: 10 20 30 40 50 
✅ Dequeued: 10
✅ Dequeued: 20
📋 Queue: 30 40 50 
✅ Enqueued: 60
✅ Enqueued: 70
📋 Queue: 30 40 50 60 70 
🔍 Element 40 found at index 3.
🔍 Element 99 not found.
```

---

### **🐍 Python Implementation**

```python
class Queue:
    def __init__(self, size):
        self.size = size
        self.queue = [None] * size # Initialize list with None
        self.front = -1
        self.rear = -1

    def is_empty(self):
        return self.front == -1

    def is_full(self):
        return (self.rear + 1) % self.size == self.front

    def enqueue(self, val):
        if self.is_full():
            print(f"🚨 Queue Overflow! Can't add {val}.")
            return
        if self.is_empty():
            self.front = 0
        self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = val
        print(f"✅ Enqueued: {val}")

    def dequeue(self):
        if self.is_empty():
            print("🚨 Queue Underflow! Nothing to remove.")
            return
        val = self.queue[self.front]
        print(f"✅ Dequeued: {val}")
        if self.front == self.rear:
            self.front = self.rear = -1 # Reset to empty state
        else:
            self.front = (self.front + 1) % self.size

    def traverse(self):
        if self.is_empty():
            print("📭 Queue is empty.")
            return
        print("📋 Queue:", end=" ")
        i = self.front
        while True:
            print(self.queue[i], end=" ")
            if i == self.rear:
                break
            i = (i + 1) % self.size
        print() # New line

    def search(self, key):
        if self.is_empty():
            print("📭 Queue is empty. Can't search.")
            return
        i = self.front
        while True:
            if self.queue[i] == key:
                print(f"🔍 Element {key} found at position {i}.")
                return
            if i == self.rear:
                break
            i = (i + 1) % self.size
        print(f"🔍 Element {key} not found.")

# Driver code
if __name__ == "__main__":
    print("🐍 Testing Queue Implementation (Python)")
    print("--------------------------------------")
    q = Queue(5) # Create a queue of size 5

    q.traverse()

    q.enqueue(10)
    q.enqueue(20)
    q.enqueue(30)
    q.enqueue(40)
    q.enqueue(50)
    q.enqueue(60) # Overflow

    q.traverse()

    q.dequeue()
    q.dequeue()

    q.traverse()

    q.enqueue(60)
    q.enqueue(70)

    q.traverse()

    q.search(40)
    q.search(99)
```
*(Output will be similar to the C++ version)*


---

## **📊 7. Summary & Key Takeaways**

| 🏷️ **Concept**              | 📖 **Description**                                  | 🎯 **Importance**                      |
| :--------------------------- | :-------------------------------------------------- | :------------------------------------- |
| **FIFO Principle**           | First-In-First-Out processing.                      | Core logic behind queues.              |
| **Linear vs Circular Queue** | Linear → False overflow ⚠️, Circular → efficient ✅. | Circular is **practical & efficient**. |
| **`front` & `rear`**         | Pointers marking start & end.                       | Essential tracking.                    |
| **Modulo `%`**               | Enables wrapping.                                   | Key to circular queue.                 |
| **Time Complexity**          | All major operations → **O(1)**.                    | Super efficient.                       |

---

## **❓ 8. Viva Voce / Interview Questions**

**Q1:** 🔄 Difference between **Stack** & **Queue**?

👉 Stack = **LIFO**, Queue = **FIFO**.

**Q2:** ⏱️ Time complexity of operations?

👉 All → **O(1)** in Circular Queue.

**Q3:** 🚨 What are **Overflow & Underflow**?

* Overflow → Inserting in a full queue.
* Underflow → Removing from an empty queue.

**Q4:** 🤔 How does **Circular Queue** fix Linear Queue?

👉 Prevents **False Overflow** by reusing empty slots.

**Q5:** 🌍 Real-world uses?

👉 CPU Scheduling, Printers, Networking Buffers, BFS, Call Centers.
