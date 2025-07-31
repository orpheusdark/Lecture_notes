
---

📘 **Lesson 14: Deque & Priority Queue**

---

🎯 **Objectives**

* Understand the **Deque (Double-Ended Queue)** and its operations.
* Learn about the **Priority Queue** and how it differs from a standard queue.
* Explore **types, implementations, and real-world use cases**.
* Analyze **common problems** and their solutions.

---

↔️ **Deque (Double-Ended Queue)**

A **Deque** (pronounced *"deck"*) allows insertion and deletion from both **front** and **rear**, unlike standard queues.

📚 **Types of Deques**

* **Input-Restricted Deque:** Insert only at rear; delete from both ends.
* **Output-Restricted Deque:** Insert at both ends; delete only from front.

🔧 **Deque Operations**

* `insertFront()` ➡️ Add at front
* `insertRear()` ➡️ Add at rear
* `deleteFront()` ❌ Remove from front
* `deleteRear()` ❌ Remove from rear
* `getFront()` 🔍 Peek front
* `getRear()` 🔍 Peek rear
* `isEmpty()` / `isFull()` ❓ Check status

🧰 **Implementation Methods**

* **Circular Array:** Uses `%` to wrap `front` and `rear` pointers.
* **Doubly Linked List:** Efficient O(1) insertions/deletions at both ends.

📌 **Use Cases**

* 🔄 **Undo/Redo** systems
* 🌐 **Browser history navigation**
* 🔁 **Palindrome checkers**
* 🧮 **Sliding window algorithms** (e.g., max in subarrays)

---

🥇 **Priority Queue**

A **Priority Queue** allows elements to be dequeued based on **priority**, not arrival order.

📋 **Rules of Operation**

* Higher-priority elements are served first.
* If priorities are equal, process by **FCFS** (First Come, First Served).

📚 **Types**

* **Min-Priority Queue (Ascending):** Lower value = higher priority.
* **Max-Priority Queue (Descending):** Higher value = higher priority.

🛠️ **Operations**

* `insert(item, priority)` ➕ Add with priority
* `deleteHighestPriority()` ❌ Remove highest priority
* `getHighestPriority()` 🔍 Peek highest priority

🧰 **Implementation Techniques**

* **Unsorted List:** Insert = O(1), Delete = O(n)
* **Sorted List:** Insert = O(n), Delete = O(1)
* **Binary Heap (Recommended):** Both Insert and Delete = O(log n)

📌 **Use Cases**

* ⚙️ **CPU Scheduling**
* 🗺️ **Dijkstra’s / Prim’s algorithms**
* 📦 **Huffman Coding (Compression)**
* 🎮 **A* Search in Games & AI*\*

---

⚠️ **Common Problems & Solutions**

### 🌀 Deque Issues

| Problem             | Description                  | Solution                         |
| ------------------- | ---------------------------- | -------------------------------- |
| **Overflow**        | Adding to a full array deque | Use dynamic array or linked list |
| **Underflow**       | Removing from empty deque    | Check `isEmpty()` before delete  |
| **Wraparound Bugs** | Front/Rear go out of bounds  | Use modulo `%` operator          |

---

### ⏳ Priority Queue Issues

| Problem                  | Description                        | Solution                                     |
| ------------------------ | ---------------------------------- | -------------------------------------------- |
| **Slow Operations**      | Arrays/lists lead to O(n)          | Use Binary Heap (O(log n))                   |
| **Duplicate Priorities** | Conflicts on same priority         | Use timestamp or insertion order             |
| **Starvation**           | Low-priority items never processed | Use **aging** to increase priority over time |

---

⏭️ Next: **Lesson 15 - Linked List**

---



