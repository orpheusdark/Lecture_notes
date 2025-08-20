# 📘 Lesson 11: **Recursion**


## 🎯 Objectives

* 🧩 Understand the fundamental concept of **Recursion**.
* 🔍 Identify the **Base Case** and **Recursive Case** in a recursive function.
* 🔁 Analyze classic recursive problems: **Factorial, GCD, Fibonacci Sequence**.
* 💻 Implement recursive solutions in **Python, C, C++, and Java**.
* ⚖️ Understand trade-offs between **recursive and iterative** solutions.

---

## 🧠 What is Recursion?

**Recursion** is a programming technique where a function calls **itself** to solve smaller instances of the same problem.
This continues until it hits the **base case** (simple scenario), after which the solution is built step by step.

### 🔑 Key Concepts

* 🛑 **Base Case:** The condition to stop recursion (prevents infinite calls).
* 🔄 **Recursive Case:** The part where the function calls itself with reduced input.

### ⏰ When to Use Recursion

* ✅ Problems **naturally recursive** (e.g., factorial, Fibonacci).
* ✅ Recursive data structures (trees, linked lists).
* ✅ Divide-and-Conquer algorithms (merge sort, quick sort).

---

## 1️⃣ Factorial

### 📌 Definition

* `n! = n * (n-1) * (n-2) * ... * 1`
* Special Case: `0! = 1`

### 🔄 Recursive Formula

* `n! = n * (n - 1)!`

### 🔁 Recursive Flow Example

```plaintext
factorial(5)
-> 5 * factorial(4)
   -> 4 * factorial(3)
      -> 3 * factorial(2)
         -> 2 * factorial(1)
            -> 1 (Base Case)
```

✅ Result: `5 * 4 * 3 * 2 * 1 = 120`

---

### ✅ Python Implementations

**Iterative Approach:**

```python
def factorial_iterative(n):
    if n < 0:
        return "Factorial is not defined for negative numbers."
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

print(f"Iterative: {factorial_iterative(5)}")  # Output: 120
```

**Recursive Approach:**

```python
def factorial_recursive(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial_recursive(n - 1)

print(f"Recursive: {factorial_recursive(5)}")  # Output: 120
```

---

## 2️⃣ Greatest Common Divisor (GCD)

### 📌 Definition

* Largest number that divides two numbers without leaving a remainder.
* Uses the **Euclidean Algorithm**.

### 🔄 Recursive Formula

* `gcd(a, b) = gcd(b, a % b)`
* **Base Case:** `gcd(a, 0) = a`

### 🔁 Recursive Flow Example

```plaintext
gcd(48, 18)
-> gcd(18, 48 % 18) = gcd(18, 12)
-> gcd(12, 18 % 12) = gcd(12, 6)
-> gcd(6, 12 % 6) = gcd(6, 0)
-> 6 (Base Case)
```

---

### ✅ C++ Implementation

```cpp
#include <iostream>
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}

int main() {
    int a = 48, b = 18;
    std::cout << "GCD of " << a << " and " << b << " is: " << gcd(a, b);
    return 0;
}
```

---

## 3️⃣ Fibonacci Sequence

### 📌 Definition

* A series where each term = sum of the two preceding ones.
* Sequence: `0, 1, 1, 2, 3, 5, 8, 13, ...`

### 🔄 Recursive Formula

* `F(n) = F(n-1) + F(n-2)`
* **Base Cases:** `F(0) = 0`, `F(1) = 1`

---

### ✅ Java Iterative Implementation

```java
import java.util.Scanner;

public class Fibonacci {
    public static void printFibonacci(int n) {
        int a = 0, b = 1, next;
        System.out.println("Fibonacci sequence up to " + n + " terms:");
        for (int i = 0; i < n; i++) {
            System.out.print(a + " ");
            next = a + b;
            a = b;
            b = next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of terms: ");
        int terms = scanner.nextInt();
        printFibonacci(terms);
    }
}
```

---

## 🧾 Summary

* 🧠 Recursion solves problems by breaking them into **smaller sub-problems**.
* 🚫 **Base case** prevents infinite recursion.
* 🔁 **Recursive case** pushes toward the base case.
* 🔍 **Factorial, GCD, Fibonacci** are classic recursion examples.
* ⚖️ Recursive vs. Iterative: recursion = cleaner code, iteration = more efficient.

---

## 📘 Viva Q\&A

❓ **Why is recursion powerful?**
👉 Because it allows us to express **complex problems** in a simpler, self-similar manner.

❓ **When should you avoid recursion?**
👉 When performance or stack memory is critical (deep inputs). Use iteration instead.

❓ **What if recursion has no base case?**
👉 Infinite recursion → leads to **stack overflow**.

❓ **How is GCD computed recursively?**
👉 Using **Euclidean Algorithm**: `gcd(a, b) = gcd(b, a % b)` until `b = 0`.

❓ **What’s the time complexity of recursive Fibonacci?**
👉 Exponential `O(2^n)` (unless optimized with memoization).

---

## ⏭️ Next Up: **Lesson 12 – Recursion with Backtracking (N-Queens, Sudoku Solver)**
