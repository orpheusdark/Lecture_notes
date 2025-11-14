
# 📘 Lesson 6: Algorithm Performance Analysis — Time & Space Complexity

## 📚 What is Algorithm Performance?

Algorithm performance is a measure of how efficiently an algorithm uses:

* **Time** (🕒 CPU cycles)
* **Space** (💾 memory)

It’s not just about how fast it runs on your computer, but how it **scales** with larger inputs.

---

### 🧠 Real-world Analogy:

Think of an algorithm like a **recipe**:

* ⏱️ **Time Complexity** → How much longer it takes to cook if you double the number of servings
* 🧂 **Space Complexity** → How many more bowls, pans, or utensils you need for more servings

---

## 🧩 Why Analyze Performance?

* ⚡ **Efficiency**: Save computing power and memory
* 📈 **Scalability**: Predict performance with large datasets
* 🧪 **Informed Decisions**: Choose the right algorithm for the job

---

## 🕒 Time Complexity & Big O Notation

Time complexity shows how the number of basic steps grows with input size **n**.

**Big O notation** focuses on worst-case growth. Constants and less significant terms are ignored.

📌 Example:
If an algorithm takes `3n² + 5n + 10` operations,
👉 Big O = **O(n²)**

---

### ⏳ Common Time Complexities:

| Complexity    | Name        | Meaning                              | Example                      |
| ------------- | ----------- | ------------------------------------ | ---------------------------- |
| 🟩 O(1)       | Constant    | Always takes same time               | Accessing array by index     |
| 🟨 O(log n)   | Logarithmic | Each step cuts problem size in half  | Binary Search                |
| 🟦 O(n)       | Linear      | Grows proportionally with input size | Looping through an array     |
| 🟪 O(n log n) | Log-Linear  | Efficient sorting                    | Merge Sort, Quick Sort (avg) |
| 🟥 O(n²)      | Quadratic   | Grows fast, slow for large inputs    | Bubble Sort, nested loops    |
| 🟥 O(2ⁿ)      | Exponential | Grows extremely fast                 | Recursive Fibonacci          |

---

## 📦 Space Complexity

Space complexity = Extra memory used (not including input).

### Examples:

* 🔒 **O(1)**: Constant space

  > e.g., Swapping two elements in-place
* 📊 **O(n)**: Linear space

  > e.g., Creating a new array of size `n`

---

## 🎭 Best, Worst, and Average Case

| Case       | Notation  | Description                          | Linear Search Example             |
| ---------- | --------- | ------------------------------------ | --------------------------------- |
| 🟢 Best    | Ω (Omega) | Minimum operations needed            | Found at index 0 → O(1)           |
| 🔴 Worst   | O (Big O) | Max operations, the common metric    | Found at end or not at all → O(n) |
| 🟡 Average | Θ (Theta) | Expected operations on typical input | Found in middle → O(n)            |

---

## ✅ Code Example: Linear Search

### 🇨 C Implementation

```c
#include <stdio.h>

int linear_search(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = 5;
    int target = 30;
    int index = linear_search(arr, n, target);
    printf("Found at index: %d\n", index);
    return 0;
}
```

* ⏱️ **Time Complexity**: O(n) — In the worst case, checks all `n` elements
* 💾 **Space Complexity**: O(1) — No extra memory based on input size

---

### 🇨++ C++ Implementation

```cpp
#include <iostream>

int linear_search(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = 5;
    int target = 30;
    int index = linear_search(arr, n, target);
    std::cout << "Found at index: " << index << std::endl;
    return 0;
}
```

---

## 📌 Summary

✅ **Time Complexity** → Runtime growth with input
✅ **Space Complexity** → Memory usage growth with input
✅ **Big O Notation** → Worst-case efficiency standard
✅ Always consider complexity — O(n²) is fine for 10 items, but disastrous for 10 million

---

## 📘 Viva Questions & Answers

> ❓ **What are time and space complexity?**
> 🅰️ Time: How runtime grows with input.
> 🅰️ Space: How memory usage grows with input.

> ❓ **What is Big O notation?**
> 🅰️ A way to describe **worst-case** algorithm performance.

> ❓ **Time complexity of linear search?**
> 🅰️ Best: O(1), Worst/Average: O(n)

> ❓ **How to compare two algorithms?**
> 🅰️ By analyzing their time and space complexities.

---

## ⏭️ Next:

📘 **Lesson 7**: Stack — Definition, Operations & Array Representation

---


