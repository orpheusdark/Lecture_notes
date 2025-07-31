
---

# 📘 Lesson 3: Arrays, Structures, Unions, and Self-Referential Structures

## 🎯 Objectives

* Understand and differentiate between four fundamental C-style data structures: Arrays, Structures, Unions, and Self-Referential Structures.
* Learn about Self-Referential Structures and their importance in building dynamic data structures.
* Analyze the memory representation and common operations for each.
* Implement basic array operations in Python and C++.

---

## 🔶 1. Arrays 🧮

An array is a linear data structure that stores a collection of elements of the same data type in **contiguous memory** locations.

### 🔹 What is a Static Array?

```cpp
// C/C++ Declaration
int arr[10];
float marks[5] = {85.5, 92.0, 78.5, 95.5, 88.0};
```

### 📌 Characteristics

* **Homogeneous**: All elements are of the same type.
* **Static Size**: Fixed during compile-time.
* **Contiguous Memory**: Efficient for caching.
* **Random Access (O(1))**: Direct access via index.
* **0-Based Indexing**: First element is at index `0`.

### 📊 Types of Arrays

| Type              | Example           |
| ----------------- | ----------------- |
| 1D Array          | `int a[5];`       |
| 2D Array (Matrix) | `int b[3][3];`    |
| Multidimensional  | `int c[2][3][4];` |

### 📈 Complexity Table (Static Arrays)

| Operation | Best | Average | Worst | Explanation     |
| --------- | ---- | ------- | ----- | --------------- |
| Access    | O(1) | O(1)    | O(1)  | Direct index    |
| Search    | O(1) | O(n)    | O(n)  | Linear scan     |
| Insertion | O(n) | O(n)    | O(n)  | Shifting needed |
| Deletion  | O(n) | O(n)    | O(n)  | Shifting needed |

### 🛠️ Use Cases

* Sequential storage
* Temporary buffers
* Lookup tables
* Return values
* Dynamic Programming (Memoization)

### 🐍 Python Code: Element Search

```python
L = list(map(int, input("Enter list elements separated by spaces: ").split()))
T = int(input("Enter the target element to search for: "))

if T in L:
    print(f"Element {T} found at index {L.index(T)}.")
else:
    print(f"Element {T} not found in the list.")
```

### 💠 C++ Code: Element Search

```cpp
#include <iostream>
int main() {
    int L[] = {1, 2, 3, 4, 5, 6};
    int T = 5;
    int n = sizeof(L) / sizeof(L[0]);
    bool found = false;

    for (int i = 0; i < n; i++) {
        if (L[i] == T) {
            std::cout << "Element " << T << " found at index " << i << "." << std::endl;
            found = true;
            break;
        }
    }

    if (!found) {
        std::cout << "Element " << T << " not found in the array." << std::endl;
    }
    return 0;
}
```

### 🔁 Dynamic Arrays

* Python `list` or C++ `std::vector`
* Automatically resizes when full.
* Amortized insertion: **O(1)**

---

## 🔶 2. Structures (struct) 🧱

Structures allow grouping of **heterogeneous data** under one name.

### 🔧 Syntax

```cpp
struct Student {
    int roll_no;
    char name[50];
    float marks;
};
```

### ✅ Usage

```cpp
struct Student s1;
s1.roll_no = 1;
strcpy(s1.name, "Ram");
s1.marks = 89.5;
```

### 📎 Features

* **Heterogeneous grouping**
* **Real-world modeling** (e.g., Students, Employees)
* **Separate memory** for each member
* **Padding** may occur for alignment

---

## 🔶 3. Unions 🧊

Unions share memory among all members.

### 🔧 Syntax

```cpp
union Data {
    int i;
    float f;
    char str[20];
};
```

### ⚙️ Features

* **Shared Memory**: Size = largest member
* **Only one active member at a time**
* **Memory-efficient**: Used in low-level systems

---

## 🔶 4. Self-Referential Structures 🔗

Structures that point to other structures of the same type.

### 🔧 Syntax

```cpp
struct Node {
    int data;
    struct Node *next;
};
```

### 🧪 Use Case: Linked List Node

```cpp
#include <stdlib.h>

struct Node *head = NULL;
head = (struct Node*) malloc(sizeof(struct Node));
head->data = 10;
head->next = NULL;
```

### 💡 Advantages

* **Dynamic structures**: Linked Lists, Trees, Graphs
* **Flexible chaining** of data

---

## 📌 Summary Table

| Feature           | Array        | Structure     | Union             | Self-Referential        |
| ----------------- | ------------ | ------------- | ----------------- | ----------------------- |
| Data Type         | Same         | Different     | Different         | Can point to same type  |
| Memory Allocation | Contiguous   | Sequential    | Shared            | Dynamic via pointers    |
| Primary Use       | Indexed data | Grouping data | Memory efficiency | Dynamic data structures |

---

## 📚 Applications in DSA

* **Arrays**: Sorting, Searching, Matrices, Stacks, Queues
* **Structures**: Records, Nodes, Parameters
* **Unions**: Low-memory systems, protocols
* **Self-Referential Structures**: Linked Lists, Trees, Graphs

---

