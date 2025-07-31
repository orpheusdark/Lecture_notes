
---

# 📘 Lesson 4: Pointers & Dynamic Memory Allocation

## 🎯 Objectives

* 🧭 Understand what pointers are in C and how they work
* 🧱 Learn the difference between static and dynamic memory allocation
* ⚙️ Master `malloc()`, `calloc()`, `realloc()`, and `free()` in C
* 🤖 Contrast C's manual memory management with Python's automatic system

---

## 📚 What are Pointers?

A **pointer** is a special variable that stores the **memory address** of another variable.

🧠 **Real-world Analogy**:
A variable is like a house with a number inside it.
A pointer is like a paper with the **address** of that house.
You follow the address to access the value inside.

### 🛠️ Pointer Operators in C

| Operator          | Description                                   |
| ----------------- | --------------------------------------------- |
| `&` (Address-of)  | Returns memory address of a variable          |
| `*` (Dereference) | Accesses value at the address held by pointer |

```c
int x = 10;
int *ptr;
ptr = &x;

printf("Value of x: %d\n", x);
printf("Address of x: %p\n", &x);
printf("Address stored in ptr: %p\n", ptr);
printf("Value at ptr: %d\n", *ptr);
```

---

## 💾 Static vs. Dynamic Memory Allocation

### 🧩 1. Static Allocation (Stack)

* 📍 Memory is allocated **at compile-time**
* ⚡ Fast but **inflexible**
* 💡 Example:

  ```c
  int arr[10];
  ```

### 🔄 2. Dynamic Allocation (Heap)

* 🕒 Allocated **at runtime**
* 🔧 Flexible but must be **manually managed**
* 💡 Example:

  ```c
  int *arr = (int*)malloc(10 * sizeof(int));
  ```

| Feature     | Static                  | Dynamic                |
| ----------- | ----------------------- | ---------------------- |
| When        | Compile-time            | Runtime                |
| Memory Area | Stack                   | Heap                   |
| Flexibility | Fixed size              | Resizable              |
| Management  | Automatic (by compiler) | Manual (by programmer) |

---

## ⚙️ Dynamic Memory Functions in C (`<stdlib.h>`)

| Function    | Purpose                             | Initializes? | Arguments                      |
| ----------- | ----------------------------------- | ------------ | ------------------------------ |
| `malloc()`  | Allocates raw memory                | ❌ No         | Total size in bytes            |
| `calloc()`  | Allocates & zero-initializes memory | ✅ Yes        | No. of elements, Size of each  |
| `realloc()` | Resizes previously allocated memory | ❌ No         | Old pointer, New size in bytes |
| `free()`    | Frees previously allocated memory   | —            | Pointer to memory block        |

📌 **Always match every `malloc()`, `calloc()`, or `realloc()` with a `free()`!**

---

## ✅ Code Examples

### 🐍 Python: Simulating Pointers & Dynamic Lists

```python
x = 10
ptr_address = id(x)
print("Value of x:", x)
print("Memory Address (ID) of x:", ptr_address)

dynamic_list = []
for i in range(5):
    dynamic_list.append(i * 2)
print("Dynamic List:", dynamic_list)
```

💡 `id(x)` gives an approximation of x’s memory address.
Python handles memory resizing automatically.

---

### 💻 C: True Pointers and Dynamic Memory

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr;
    int n = 5;

    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        arr[i] = i * 2;
        printf("arr[%d] = %d\n", i, arr[i]);
    }

    free(arr);
    arr = NULL;
    return 0;
}
```

🧠 **Key Points**:

* `malloc()` allocates raw memory.
* Always check if `malloc()` returns `NULL`.
* `arr[i]` is shorthand for `*(arr + i)`.
* Always `free()` and set pointer to `NULL`.

---

## 🧠 Summary & Key Takeaways

* 🧭 **Pointers** allow direct memory access and manipulation.
* 🔐 **Static memory** is fast but inflexible (allocated on stack).
* 🔓 **Dynamic memory** is flexible (allocated on heap) but must be freed manually.
* ⚠️ Avoid memory leaks by **always calling `free()`**.
* 🐍 Python does all this under the hood with garbage collection—safe, but less powerful.

---

## 📘 Viva Q\&A

**Q1. What is a pointer?**
A pointer is a variable that stores the memory address of another variable.

**Q2. Difference between `malloc()` and `calloc()`?**

* `malloc()` allocates uninitialized memory (garbage values)
* `calloc()` allocates memory and initializes it to zero
* `malloc(n * size)` vs. `calloc(n, size)`

**Q3. Role of `free()`?**
It deallocates heap memory, making it reusable and preventing memory leaks.

**Q4. What happens if you don’t free dynamic memory?**
🧨 Memory leak! The memory stays reserved and unavailable, leading to performance issues and crashes over time.

---

## ⏭️ Next:

📘 **Lesson 5 – Stack: Concepts and Operations**

---


