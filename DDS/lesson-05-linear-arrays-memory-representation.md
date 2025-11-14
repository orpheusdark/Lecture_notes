
---

# 📘 Lesson 5: Representation of Linear Arrays in Memory


## 📚 What is a Linear Array?

A **linear array** is a collection of elements of the same type stored in a **single, contiguous block of memory**.
This sequential layout is why arrays are lightning-fast for access.

### 🧠 Real-world Analogy

Imagine a row of **mailboxes**, each with a number (index).
If you know where the first one is, you can find the rest by just walking down the row.

---

## 📦 Contiguous Memory Allocation

All elements are placed one after another in memory.
If the base address of `arr[0]` is `B`, the formula to calculate any `arr[i]` is:

```
Address of arr[i] = B + (i × size_of_data_type)
```

This provides **O(1)** (constant time) access.

### 🧮 Example

```c
int arr[5] = {10, 20, 30, 40, 50};
```

Assume:

* Base Address = `1000`
* `sizeof(int)` = `4 bytes`

| Index | Value | Formula    | Address |
| ----- | ----- | ---------- | ------- |
| 0     | 10    | 1000 + 0×4 | 1000    |
| 1     | 20    | 1000 + 1×4 | 1004    |
| 2     | 30    | 1000 + 2×4 | 1008    |
| 3     | 40    | 1000 + 3×4 | 1012    |
| 4     | 50    | 1000 + 4×4 | 1016    |

---

## ✅ Code Demonstrations

### 💻 C Implementation

```c
#include <stdio.h>

int main() {
    int arr[5] = {10, 20, 30, 40, 50};

    printf("Demonstrating contiguous memory in C:\n");
    for (int i = 0; i < 5; i++) {
        printf("Index: %d, Value: %d, Address: %p\n", i, arr[i], (void*)&arr[i]);
    }

    return 0;
}
```

#### 🔍 Line-by-Line Explanation

* `#include <stdio.h>` — Required for `printf()`
* `int arr[5] = ...` — Static array, memory allocated on **stack**
* `&arr[i]` — Gets address of the `i-th` element
* `(void*)` — Cast for proper printing with `%p` (pointer)

---

### 💻 C++ Implementation

```cpp
#include <iostream>

int main() {
    int arr[5] = {10, 20, 30, 40, 50};

    std::cout << "Demonstrating contiguous memory in C++:\n";
    for (int i = 0; i < 5; i++) {
        std::cout << "Index: " << i
                  << ", Value: " << arr[i]
                  << ", Address: " << &arr[i] << std::endl;
    }

    return 0;
}
```

#### 🔍 Highlights

* `std::cout` is used instead of `printf()`
* `&arr[i]` works exactly the same
* `std::endl` ensures newline and flushes output

---

### 🐍 Python Note: Memory Management

In **Python**, lists store **references**, not raw values. To simulate C-like arrays:

```python
import array

arr = array.array('i', [10, 20, 30, 40, 50])

print("Demonstrating object IDs in a Python array:")
print("Index\tValue\tMemory ID")
for i in range(len(arr)):
    print(f"{i}\t{arr[i]}\t{id(arr[i])}")
```

#### 🔍 Explanation:

* `array.array('i', ...)` creates a **type-restricted**, memory-efficient array
* `id()` returns a unique object ID (approximate memory address in CPython)
* Unlike C, the data isn’t guaranteed to be packed side-by-side at machine level

---

## ✅ Summary

| Feature              | C / C++                      | Python                             |
| -------------------- | ---------------------------- | ---------------------------------- |
| Storage              | Contiguous memory            | Contiguous references              |
| Element Access Time  | O(1) via address calculation | O(1) for list indices              |
| Control              | Full memory control          | Abstracted by Python VM            |
| Low-level Visibility | Yes                          | No (except with `ctypes`, `array`) |

### 📌 Key Point:

Arrays = **Contiguous Blocks** → Enable **fast random access** → Optimize CPU cache usage

---

## 📘 Viva Questions & Answers

**Q1. How are arrays stored in memory?**
In a contiguous block, where each element sits directly after the previous one.

**Q2. How to calculate the address of `arr[i]`?**
`Address = Base + i × sizeof(type)`

**Q3. Why is contiguous allocation important?**
It allows for:

* **O(1)** random access
* **Better cache performance**

**Q4. How does Python handle arrays differently?**
Python lists store **pointers to objects** contiguously, not the values themselves.
Use `array` module for memory-efficient storage.

---

## ⏭️ Next:

📘 **Lesson 6 – Algorithm Performance Analysis: Time & Space Complexity**

---



