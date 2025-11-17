# 🛠️ Linked List Operations in C++

---

## 🚀 Why Linked Lists?

Before we dive into operations, remember *why* we use linked lists!

👉 Unlike **arrays**, which are like a fixed-size train 🚂 (where adding a new car in the middle is a nightmare), **linked lists** are like a treasure hunt 🗺️. Each clue tells you where to find the next one.

This makes them **super-efficient** for **adding** or **removing "clues" (nodes)** anywhere in the chain — you only need to update a couple of pointers!

✅ **Advantages:** Dynamic size, `O(1)` insertions/deletions (at known positions).
⚠️ **Disadvantages:** No random access (`O(n)` access time), extra memory for pointers.

---

## 🧱 The Blueprint: Node Structure in C++

Everything in a linked list starts with this **fundamental building block** 👇

```cpp
// Define the Node structure
struct Node {
    int data;   // The value stored in the node (can be any data type)
    Node* next; // Pointer to the next node in the sequence

    // Constructor to easily initialize a new node (Optional but very helpful!)
    Node(int data) : data(data), next(nullptr) {}
};
```

🔑 **Breakdown:**

* `data`: Holds the actual value (e.g., `5`, `10`, `42`).
* `next`: A **crucial pointer** storing the memory address of the next node.

  * If it’s the last node ➝ points to `nullptr` (means *end of the list*).

---

## 🔁 Operation 1: Traversing the List

🎯 **Goal:** Visit every single node from the `head` to the end, usually to **print values** 🖨️.

### 🧠 Logic & Algorithm

1. Start with a **temporary pointer** (`temp`) pointing to `head`.
2. Continue looping **while `temp` is not `nullptr`**.
3. Inside the loop:

   * **Process** the current node (e.g., print `temp->data`).
   * **Move** to the next node (`temp = temp->next`).

📊 **Visualization:**

```
[Head] -> [10] -> [20] -> [30] -> nullptr
  ^ 
(temp)

Print "10", then move temp ➝ next
```

### 💻 C++ Implementation

```cpp
void traverse(Node* head) {
    Node* temp = head; // Start from the head
    std::cout << "Linked List: ";

    while (temp != nullptr) { // Traverse until the end
        std::cout << temp->data << " -> ";
        temp = temp->next; // Move to the next node
    }
    std::cout << "NULL" << std::endl; // End of the list
}
```

---

## 🔍 Operation 2: Searching for a Key

🎯 **Goal:** Check if a specific value (`key`) exists in the list 🔎.

### 🧠 Logic & Algorithm

1. Start with `temp` pointing to `head`.
2. Loop while `temp != nullptr`.
3. Inside loop:

   * If `temp->data == key` ➝ return **true** 🎉.
   * Else, move to `temp->next`.
4. If loop ends ➝ return **false** 😞.

### 💻 C++ Implementation

```cpp
bool search(Node* head, int key) {
    Node* temp = head;

    while (temp != nullptr) {
        if (temp->data == key) {
            return true; // ✅ Key found
        }
        temp = temp->next; // Move ahead
    }
    return false; // ❌ Key not found
}
```

---

## ➕ Operation 3: Inserting a Node

👉 Insertion can be at **beginning, middle, or end**.
Here, we focus on the most common one: **Insert at the Beginning**.

🎯 **Goal:** Add a new node at the **front**, making it the new `head`.

### 🧠 Logic & Algorithm

1. **Create** a new node with the given data.
2. **Link** the new node ➝ set `newNode->next = head`.

   * (This step is **VITAL** ⚡ to avoid losing the rest of the list).
3. **Update** head pointer ➝ `head = newNode`.

📊 **Visualization:**

```
Step 0: [Head] -> [10] -> [20] -> NULL

Step 1: [NewNode:5] -> [10] -> [20] -> NULL

Step 2: [Head] -> [5] -> [10] -> [20] -> NULL
```

### 💻 C++ Implementation

```cpp
// Head passed by reference (Node*&) so we can update it
void insertAtBeginning(Node*& head, int newData) {
    Node* newNode = new Node(newData); // 1. Create node
    newNode->next = head;              // 2. Link to list
    head = newNode;                    // 3. Update head
}
```

---

## ❌ Operation 4: Deleting a Node

🎯 **Goal:** Remove the **first node** that contains a given `key` and re-link the list properly.

### 🧠 Logic & Algorithm

1. **Check if list empty** ➝ If yes, return.
2. **Special Case:** If `head` itself holds the key ➝ update `head` and delete old node.
3. **General Case:**

   * Traverse with two pointers: `prev` & `current`.
   * Stop when `current->data == key`.
   * Re-link ➝ `prev->next = current->next`.
   * Delete `current`.

📊 **Visualization (Delete 20):**

```
Before: [Head] -> [10] -> [20] -> [30] -> NULL
           ^        ^
         (prev)   (current)

After:  [Head] -> [10] ------> [30] -> NULL
              \ 
               X (20 deleted)
```

### 💻 C++ Implementation

```cpp
void deleteNode(Node*& head, int key) {
    if (head == nullptr) return; // 1. Empty list

    Node* temp = head;
    Node* prev = nullptr;

    // 2. Special Case: head node
    if (temp != nullptr && temp->data == key) {
        head = temp->next;
        delete temp;
        return;
    }

    // 3. Traverse to find the key
    while (temp != nullptr && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == nullptr) return; // ❌ Not found

    prev->next = temp->next; // Unlink
    delete temp; // Free memory
}
```

---

## 🧩 Putting It All Together: Full Code Example

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int data) : data(data), next(nullptr) {} // Constructor
};

// ... [Insert functions from above here] ...

int main() {
    Node* head = nullptr; // Start empty

    insertAtBeginning(head, 30);
    insertAtBeginning(head, 20);
    insertAtBeginning(head, 10);

    std::cout << "After insertion:\n";
    traverse(head); // 10 -> 20 -> 30 -> NULL

    std::cout << "\nSearching for 20: " << (search(head, 20) ? "Found!" : "Not Found!") << std::endl;
    std::cout << "Searching for 99: " << (search(head, 99) ? "Found!" : "Not Found!") << std::endl;

    deleteNode(head, 20);
    std::cout << "\nAfter deleting 20:\n";
    traverse(head); // 10 -> 30 -> NULL

    deleteNode(head, 10); 
    std::cout << "After deleting 10 (head):\n";
    traverse(head); // 30 -> NULL

    return 0;
}
```

---

## ⏱️ Time Complexity Analysis

| Operation                 | Worst-Case | Explanation                                         |
| ------------------------- | ---------- | --------------------------------------------------- |
| **Traverse** 🛤️          | O(n)       | Must visit every node.                              |
| **Search** 🔎             | O(n)       | Might check all nodes.                              |
| **Insert at Beginning** ➕ | O(1)       | Constant-time.                                      |
| **Delete** ❌              | O(n)       | Traverse to find node (but deletion itself = O(1)). |

---

## 🎯 Conclusion: Practice Makes Perfect

👉 Always **draw diagrams** 🖊️ of nodes & pointers *before/after* operations. This helps avoid pointer mistakes and builds strong intuition.

📚 These operations are the **building blocks** for advanced structures like:

* **Stacks** 📦
* **Queues** 🎟️
* **Graphs** 🌐

So keep practicing 🔥!

---
