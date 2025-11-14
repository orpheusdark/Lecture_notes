# 🔗 **LAB 6: Mastering Singly Linked Lists & Operations**

## 📜 **1. Introduction: The Limitation of Arrays & The Need for Linked Lists**

Imagine you're organizing a **treasure hunt 🗺️** where each clue points to the location of the next one.
This chain of clues is very **flexible** — you can easily **add** a new clue in the middle or **remove** one without disrupting the entire hunt. 👉 This is the **core idea behind a Linked List**.

💡 In programming, while **arrays** are great, they have a big limitation:

* **Static memory allocation** – you must declare their size upfront.
* If you need more elements ➝ you **can’t easily expand** the array.
* If you declare it too large ➝ you **waste memory**.

✨ **The Solution: Dynamic Data Structures!**
A **Singly Linked List** is a linear data structure where each element (called a **Node**) contains:

* **Data** 📝 → the value to be stored.
* **Next** 🔗 → a pointer/reference to the next node in the sequence.

➡️ This allows **efficient insertion & deletion** at any position (no shifting like in arrays).
➡️ Memory is **allocated dynamically** for each new node.

---

## 🎯 **2. The Problem & Why Linked Lists Shine**

⚡ **The Core Challenge:** Managing data collections where:

* The size is **unpredictable**, or
* Frequent **insertions/deletions** (especially in the middle) are expected.

🔑 **Operations Where Linked Lists Excel (vs Arrays):**

* **Insertion at Beginning** ➝ O(1) ✅ vs Array O(n) ❌
* **Deletion at Beginning** ➝ O(1) ✅ vs Array O(n) ❌
* **Insertion/Deletion at Known Position** ➝ O(1)\* (\*after reaching position)

  * But **finding the position** takes O(n).

📌 **Real-World Applications:**

* 📚 **Stacks & Queues** → dynamic size flexibility.
* 🖼️ **Image Viewer** → "next" and "previous" navigation.
* 🎵 **Music Playlist** → easy add/remove of tracks.
* 🌐 **Web Browsing History** → back/forward using **doubly linked list**.
* 🖥️ **Memory Management (OS)** → track free memory blocks.
* ✍️ **Undo Functionality** (Word, Photoshop) → each action is a node.

---

## 🏗️ **3. Understanding the Node Structure**

🔹 A **Node** is the **building block** of a linked list.
🔹 In memory, nodes are **not contiguous** – they’re scattered, each holding:
`[ Data | Next ]`

📌 **Visualization:**

```
[ Data | Next ] ---> [ Data | Next ] ---> [ Data | NULL ]
```

➡️ The **last node’s next = NULL**, marking the **end of the list**.

---

## 🧠 **4. Logic Building & Core Operations (Step-by-Step)**

We’ll use a sample list:
👉 `5 -> 10 -> 20 -> NULL`

---

### 1️⃣ **Insertion at the Beginning** `insertAtBeginning(3)`

**Goal:** Add `3` at the start.

**Logic:**

1. Create new node → `newNode.data = 3`.
2. Make `newNode.next = head`.
3. Update head → `head = newNode`.

✅ **Result:** `3 -> 5 -> 10 -> 20 -> NULL`
⏱️ **Complexity:** O(1).

---

### 2️⃣ **Insertion at the End** `insertAtEnd(25)`

**Goal:** Add `25` at the end.

**Logic:**

1. Create new node → `newNode.data = 25; newNode.next = NULL`.
2. If list empty → `head = newNode`.
3. Else → Traverse till last node.
4. Make last node’s `next = newNode`.

✅ **Result:** `5 -> 10 -> 20 -> 25 -> NULL`
⏱️ **Complexity:** O(n).

---

### 3️⃣ **Deletion by Value** `deleteNode(10)`

**Goal:** Remove node with value `10`.

**Logic:**

* If empty → nothing to delete.
* If head node = key:

  * `temp = head`
  * `head = head.next`
  * `delete temp`
* Else traverse list:

  * Find node `curr` with value.
  * Track previous node `prev`.
  * `prev.next = curr.next`.
  * `delete curr`.

✅ **Result:** `5 -> 20 -> NULL`
⏱️ **Complexity:** O(n).

---

### 4️⃣ **Traversal** `traverse()`

**Goal:** Print all elements.

**Logic:**

* Start from head.
* While not NULL:

  * Print `current.data`.
  * Move → `current = current.next`.

⏱️ **Complexity:** O(n).

---

### 5️⃣ **Search** `search(20)`

**Goal:** Check if value exists.

**Logic:** Traverse list → compare each node’s data with key. Return `true` if found.

⏱️ **Complexity:** O(n).

---

### 6️⃣ **Reversal** `reverse()`

**Goal:** Reverse entire list.

**Logic (3 pointers):**

1. Initialize → `prev = NULL, curr = head, next = NULL`.
2. Iterate:

   * `next = curr->next`
   * `curr->next = prev`
   * `prev = curr`
   * `curr = next`
3. New head = `prev`.

📌 **Visualization:**

```
Original: 5 -> 10 -> 20 -> NULL
Step 1: NULL <- 5 | 10 -> 20 -> NULL (prev=5, curr=10)
Step 2: NULL <- 5 <- 10 | 20 -> NULL (prev=10, curr=20)
Step 3: NULL <- 5 <- 10 <- 20 | NULL (prev=20, curr=NULL)
Final: 20 -> 10 -> 5 -> NULL
```

⏱️ **Complexity:** O(n).

---

## **💻 5. Code Implementation & Explanation**

### **C++ Implementation (Object-Oriented with Pointers)**

```cpp
#include <iostream>
using namespace std;

// Blueprint for a Node
struct Node {
    int data;       // Value stored in the node
    Node* next;     // Pointer to the next node
};

class LinkedList {
    Node* head;     // Pointer to the first node of the list

public:
    // Constructor: Initializes an empty list
    LinkedList() {
        head = nullptr; // nullptr is modern C++ for NULL
    }

    // Operation 1: Insert at the End
    void insertAtEnd(int val) {
        Node* newNode = new Node; // 1. Create new node
        newNode->data = val;      // 2. Assign data
        newNode->next = nullptr;  // 3. It will be the last node

        if (head == nullptr) {    // If list is empty
            head = newNode;       //   new node becomes the head
        } else {
            Node* temp = head;
            while (temp->next != nullptr) { // 4. Traverse to the last node
                temp = temp->next;
            }
            temp->next = newNode; // 5. Link the last node to the new node
        }
        cout << "✅ Inserted " << val << " at the end." << endl;
    }

    // Operation 2: Insert at the Beginning
    void insertAtBeginning(int val) {
        Node* newNode = new Node; // 1. Create new node
        newNode->data = val;      // 2. Assign data
        newNode->next = head;     // 3. New node points to current head
        head = newNode;           // 4. Head now points to the new node
        cout << "✅ Inserted " << val << " at the beginning." << endl;
    }

    // Operation 3: Delete by Value
    void deleteNode(int key) {
        if (head == nullptr) { // Check for empty list
            cout << "🚨 List is empty. Cannot delete." << endl;
            return;
        }

        Node* temp = head;
        Node* prev = nullptr;

        // Case 1: If head node itself holds the key
        if (temp != nullptr && temp->data == key) {
            head = temp->next; // Change head to next node
            delete temp;       // Free the old head's memory
            cout << "✅ Deleted " << key << " from the list." << endl;
            return;
        }

        // Case 2: Search for the key to be deleted
        while (temp != nullptr && temp->data != key) {
            prev = temp;
            temp = temp->next;
        }

        if (temp == nullptr) { // Key was not present in list
            cout << "🔍 Element " << key << " not found for deletion." << endl;
            return;
        }

        // Unlink the node from the linked list
        prev->next = temp->next;
        delete temp; // Free memory
        cout << "✅ Deleted " << key << " from the list." << endl;
    }

    // Operation 4: Traverse and Display
    void traverse() {
        if (head == nullptr) {
            cout << "📭 The list is empty." << endl;
            return;
        }
        Node* temp = head;
        cout << "📋 Linked List: ";
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }

    // Operation 5: Search for an Element
    void search(int key) {
        Node* temp = head;
        int position = 0;
        while (temp != nullptr) {
            if (temp->data == key) {
                cout << "🔍 Element " << key << " found at position " << position << "." << endl;
                return;
            }
            temp = temp->next;
            position++;
        }
        cout << "🔍 Element " << key << " not found in the list." << endl;
    }

    // Operation 6: Reverse the List (Iterative Method)
    void reverse() {
        Node* prev = nullptr;
        Node* curr = head;
        Node* next = nullptr;

        while (curr != nullptr) {
            next = curr->next; // Store next node
            curr->next = prev; // Reverse current node's pointer
            prev = curr;       // Move prev one step forward
            curr = next;       // Move curr one step forward
        }
        head = prev; // Reset head to the new first node
        cout << "🔄 List has been reversed." << endl;
    }

    // Destructor: Important to free all allocated memory
    ~LinkedList() {
        Node* temp = head;
        while (temp != nullptr) {
            Node* nextNode = temp->next;
            delete temp;
            temp = nextNode;
        }
    }
};

int main() {
    cout << "🧪 Testing Singly Linked List Implementation (C++)" << endl;
    cout << "-------------------------------------------------" << endl;

    LinkedList myList;

    myList.traverse(); // Display empty list

    myList.insertAtEnd(10);
    myList.insertAtEnd(20);
    myList.insertAtBeginning(5); // List: 5 -> 10 -> 20 -> NULL
    myList.traverse();

    myList.search(20);
    myList.search(99);

    myList.deleteNode(10); // List: 5 -> 20 -> NULL
    myList.traverse();

    myList.reverse();      // List: 20 -> 5 -> NULL
    myList.traverse();

    myList.insertAtBeginning(1); // List: 1 -> 20 -> 5 -> NULL
    myList.traverse();

    return 0;
    // Destructor is automatically called here, freeing all memory
}
```
**Expected Output:**
```
🧪 Testing Singly Linked List Implementation (C++)
-------------------------------------------------
📭 The list is empty.
✅ Inserted 10 at the end.
✅ Inserted 20 at the end.
✅ Inserted 5 at the beginning.
📋 Linked List: 5 -> 10 -> 20 -> NULL
🔍 Element 20 found at position 2.
🔍 Element 99 not found in the list.
✅ Deleted 10 from the list.
📋 Linked List: 5 -> 20 -> NULL
🔄 List has been reversed.
📋 Linked List: 20 -> 5 -> NULL
✅ Inserted 1 at the beginning.
📋 Linked List: 1 -> 20 -> 5 -> NULL
```

### **Python Implementation**

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
        else:
            temp = self.head
            while temp.next is not None:
                temp = temp.next
            temp.next = new_node
        print(f"✅ Inserted {data} at the end.")

    def insert_at_beginning(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        print(f"✅ Inserted {data} at the beginning.")

    def delete_node(self, key):
        if self.head is None:
            print("🚨 List is empty. Cannot delete.")
            return

        # If head node is the node to be deleted
        if self.head.data == key:
            temp = self.head
            self.head = self.head.next
            temp = None # Python's garbage collector will handle this
            print(f"✅ Deleted {key} from the list.")
            return

        # Search for the node to be deleted
        temp = self.head
        prev = None
        while temp is not None and temp.data != key:
            prev = temp
            temp = temp.next

        if temp is None:
            print(f"🔍 Element {key} not found for deletion.")
            return

        # Unlink the node
        prev.next = temp.next
        temp = None
        print(f"✅ Deleted {key} from the list.")

    def traverse(self):
        if self.head is None:
            print("📭 The list is empty.")
            return
        temp = self.head
        print("📋 Linked List: ", end="")
        while temp is not None:
            print(temp.data, end=" -> ")
            temp = temp.next
        print("NULL")

    def search(self, key):
        temp = self.head
        position = 0
        while temp is not None:
            if temp.data == key:
                print(f"🔍 Element {key} found at position {position}.")
                return
            temp = temp.next
            position += 1
        print(f"🔍 Element {key} not found in the list.")

    def reverse(self):
        prev = None
        curr = self.head
        while curr is not None:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        self.head = prev
        print("🔄 List has been reversed.")


# Driver Code
if __name__ == "__main__":
    print("🐍 Testing Singly Linked List Implementation (Python)")
    print("----------------------------------------------------")
    ll = SinglyLinkedList()

    ll.traverse()

    ll.insert_at_end(10)
    ll.insert_at_end(20)
    ll.insert_at_beginning(5)
    ll.traverse()

    ll.search(20)
    ll.search(99)

    ll.delete_node(10)
    ll.traverse()

    ll.reverse()
    ll.traverse()

    ll.insert_at_beginning(1)
    ll.traverse()
```
*(Output will be similar to the C++ version)*

---

## **📊 6. Summary & Key Takeaways**

| Concept | Description | Importance |
| :--- | :--- | :--- |
| **Dynamic Size** | Grows and shrinks at runtime as needed. | Solves the fixed-size problem of arrays. |
| **Efficient Insertion/Deletion** | O(1) at head, O(n) at tail (without tail pointer) or specific position. | Better than arrays (O(n)) for operations at the head. |
| **Memory Usage** | Uses extra memory for pointers. | Trade-off for flexibility. |
| **Traversal** | Accessing an element by index is O(n). | Slower than arrays (O(1)) for random access. |
| **Head Pointer** | Crucial for accessing the entire list. | Losing the head means losing the list (memory leak). |

---

## **❓ 7. Viva Voce / Interview Questions**

**Q1: What is a linked list and how is it different from an array?**
*   **A:** A linked list is a linear data structure where elements are stored in non-contiguous memory locations and are linked using pointers. Unlike arrays, linked lists are dynamic in size and facilitate efficient insertions/deletions, but they have slower access time for arbitrary elements.

**Q2: What are the advantages and disadvantages of linked lists over arrays?**
*   **Advantages:**
    *   Dynamic size.
    *   Efficient insertion/deletion (especially at the beginning).
*   **Disadvantages:**
    *   Random access is not allowed. Access is sequential.
    *   Extra memory space is required for pointers.
    *   Not cache-friendly, as nodes are not contiguous in memory.

**Q3: Explain the process of reversing a linked list.**
*   **A:** The iterative method uses three pointers: `prev`, `curr`, and `next`. Initialize `prev` as `NULL` and `curr` as `head`. Traverse the list. In each iteration, store the `next` node, reverse the `curr` node's pointer to point to `prev`, then move `prev` and `curr` one step forward. Finally, set `head` to `prev`.

**Q4: What is the time complexity of various operations in a singly linked list?**
*   **Access (by index):** O(n)
*   **Search:** O(n)
*   **Insertion/Deletion at head:** O(1)
*   **Insertion/Deletion at tail:** O(n) (without a tail pointer)
*   **Insertion/Deletion at a given position:** O(n) (time to find the position)

**Q5: What is a memory leak, and why is it important to manage memory in languages like C++?**
*   **A:** A memory leak occurs when a program allocates memory (e.g., using `new` in C++) but fails to release it (using `delete`). Over time, this consumes all available memory, leading to sluggish performance or crashes. It's crucial to have a destructor in the LinkedList class that traverses the list and deletes every node. Languages like Python and Java have automatic garbage collection to handle this.
