
---

# 📘 Lesson 2: Primitive vs Non-Primitive Data Structures

## 🧩 What are Primitive Data Structures?

Primitive data structures are the most **basic data types** directly supported by a programming language. They are the **building blocks** for all other structures.

### 🔑 Key Characteristics:

* ⚛️ **Atomic**: Represent a single value (e.g., `10`, `'A'`)
* 🏗️ **Predefined**: Built into the language, no imports needed
* 💾 **Value Types**: Store the actual value in memory (in languages like C, C++, Java)

### 🧪 Common Examples:

* `int` – Whole numbers (e.g., `-5`, `0`, `100`)
* `float`, `double` – Decimal numbers (e.g., `3.14`, `-0.001`)
* `char` – Single characters (e.g., `'a'`, `'%'`, `'7'`)
* `bool` – Logical values (`true`, `false`)

---

## 🏗️ What are Non-Primitive Data Structures?

Non-primitive (or composite) data structures are **programmer-defined** and built using primitives. They store **collections** of related data.

### 🔑 Key Characteristics:

* 🧱 **Derived**: Constructed from primitives (e.g., array of `int`s)
* 🧠 **Complex**: Store multiple values and provide operations
* 🧭 **Reference Types**: Store **addresses**, not actual values (especially in Python, Java)

### 🗂️ Classification:

#### 📏 **Linear Data Structures**:

Elements are arranged in a **sequence**.
Examples:

* 📚 Arrays
* 📋 Lists
* 📦 Stacks
* 🧾 Queues
* 🔗 Linked Lists

#### 🌐 **Non-Linear Data Structures**:

Elements are arranged in **hierarchies or graphs**.
Examples:

* 🌲 Trees
* 🕸️ Graphs
* 🗻 Heaps

---

## 🐍 Python Implementation

In Python, the distinction centers around **mutability** and whether an object holds a **single value** or a **collection**.

### 🧑‍💻 Python Code

```python
# ✅ Primitive data types in Python
# These are immutable objects holding single values.
num = 10          # int
pi = 3.14         # float
initial = 'A'     # str (Python doesn't have a separate char type)
is_valid = True   # bool

# ✅ Non-primitive: List (a linear data structure)
# This is a mutable object holding a collection of other objects.
students = ["Ali", "Sara", "Zaid"]

# Accessing elements by index (a key feature of linear structures)
print("Student at index 1:", students[1])

# Adding a new student
students.append("Hina")

# Traversing (visiting each element in) the list
print("📋 Student List:")
for name in students:
    print("-", name)
```

### 🧠 Line-by-Line Explanation:

* `num = 10`: `num` references an integer object with value 10
* `pi = 3.14`: `pi` holds a reference to a float object
* `initial = 'A'`: Single characters are `str` in Python
* `is_valid = True`: Boolean value assigned
* `students = [...]`: A list of string references
* `print(...)`: Accesses and prints the second student
* `students.append(...)`: Adds "Hina" to the list
* `for name in students:`: Iterates and prints each student

---

## 🇨 C Implementation

In **C**, primitives and non-primitives are **clearly defined** and tied to **memory layout**.

### 🧑‍💻 C Code

```c
#include <stdio.h>
#include <stdbool.h> // Include for bool type (from C99 standard)

int main() {
    // ✅ Primitive data types
    // These variables directly store their values in memory.
    int num = 10;
    float pi = 3.14;
    char initial = 'A';
    bool is_valid = true;

    // ✅ Non-primitive: Array (a linear data structure)
    // 'students' is a block of memory holding 4 arrays of 20 chars each.
    char students[4][20] = {"Ali", "Sara", "Zaid", "Hina"};

    // Accessing an element
    printf("Student at index 1: %s\n", students[1]);

    // Traversing the array
    printf("Student List:\n");
    for (int i = 0; i < 4; i++) {
        printf("- %s\n", students[i]);
    }

    return 0;
}
```

### 🧠 Line-by-Line Explanation:

* `#include <stdbool.h>`: Enables `bool`, `true`, `false` (from C99)
* `int num = 10;`: Allocates memory for an integer
* `float pi = 3.14;`: Stores a decimal value
* `char initial = 'A';`: Stores ASCII representation
* `char students[4][20] = ...;`: Allocates 80 bytes for 4 strings
* `printf(..., students[1]);`: Prints second string `"Sara"`
* `for (...)`: Iterates over all students in array

---

## ✅ Summary

* **Primitive types** (`int`, `float`, `char`) store **single atomic values** directly in memory
* **Non-primitive types** (e.g., arrays, lists, trees) are **collections**, often stored using **references or pointers**

📌 Understanding this distinction is essential for:

* Efficient memory usage
* Data manipulation strategies
* Performance optimization

---

## ⏭️ Coming Up Next:

**Lesson 3**: 📊 **Arrays and Memory Representation** (with Python lists and C arrays)

---


