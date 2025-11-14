# 📘 Lesson 12: **Recursion – The Tower of Hanoi**


## 🗼 What is the Tower of Hanoi?

The **Tower of Hanoi** is a mathematical puzzle consisting of **three rods** and a number of **disks of different sizes**.

* The puzzle starts with the disks stacked in ascending size on one rod (the **source**), with the smallest disk at the top.
* 🎯 **Goal:** Move the entire stack to another rod (the **destination**) using the third rod as an **auxiliary** (temporary placeholder).

### 📏 Rules

* 1️⃣ Only **one disk** can be moved at a time.
* 🔝 A move involves taking the **upper disk** from a stack and placing it on top of another stack or an empty rod.
* 🚫 No disk may be placed on top of a **smaller disk**.

---

## 🧠 The Recursive Strategy

The Tower of Hanoi problem is a **textbook example of recursion**.
To move `n` disks from rod `A` (source) to rod `C` (destination) using rod `B` (auxiliary):

1. 🔁 Move `n-1` disks from `A` → `B` using `C`.
2. ➡️ Move the `nth` (largest) disk from `A` → `C`.
3. 🔁 Move `n-1` disks from `B` → `C` using `A`.

📌 **Base Case:**
If `n == 1`, move the disk directly from source to destination.

---

## 🧮 Walkthrough Example (n = 3 Disks: A → C)

1. Move 2 disks from A → B:

   * Move disk 1 from A → C
   * Move disk 2 from A → B
   * Move disk 1 from C → B

2. Move 1 disk from A → C:

   * Move disk 3 from A → C

3. Move 2 disks from B → C:

   * Move disk 1 from B → A
   * Move disk 2 from B → C
   * Move disk 1 from A → C

✅ Now all disks are stacked on rod **C** in correct order.

---

## 🔢 Number of Moves

The **minimum number of moves** required for `n` disks is:

📐 **Formula:** `2^n - 1`

* For 3 disks → `2³ - 1 = 7 moves`
* For 4 disks → `2⁴ - 1 = 15 moves`

---

## ✅ Code Implementations

### 📌 C Implementation

```c
#include <stdio.h>

void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {
    if (n == 1) {
        printf("Move disk 1 from rod %c to rod %c\n", from_rod, to_rod);
        return;
    }
    towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);
    printf("Move disk %d from rod %c to rod %c\n", n, from_rod, to_rod);
    towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
}

int main() {
    int n = 3;
    printf("Steps to solve Tower of Hanoi for %d disks:\n", n);
    towerOfHanoi(n, 'A', 'C', 'B');
    return 0;
}
```

🔍 **Explanation:**

* 🧱 **Base case:** `n == 1` → move directly.
* 🪜 **Recursive steps:** Move `n-1` disks → move largest → move `n-1` disks again.

---

### 🐍 Python Implementation

```python
def tower_of_hanoi(n, from_rod, to_rod, aux_rod):
    if n == 1:
        print(f"Move disk 1 from rod {from_rod} to rod {to_rod}")
        return
    tower_of_hanoi(n - 1, from_rod, aux_rod, to_rod)
    print(f"Move disk {n} from rod {from_rod} to rod {to_rod}")
    tower_of_hanoi(n - 1, aux_rod, to_rod, from_rod)

# --- Test Case ---
num_disks = 3
print(f"Steps to solve Tower of Hanoi for {num_disks} disks:")
tower_of_hanoi(num_disks, 'A', 'C', 'B')
```

---

### ☕ Java Implementation

```java
public class TowerOfHanoi {

    public static void solve(int n, char fromRod, char toRod, char auxRod) {
        if (n == 1) {
            System.out.println("Move disk 1 from rod " + fromRod + " to rod " + toRod);
            return;
        }
        solve(n - 1, fromRod, auxRod, toRod);
        System.out.println("Move disk " + n + " from rod " + fromRod + " to rod " + toRod);
        solve(n - 1, auxRod, toRod, fromRod);
    }

    public static void main(String[] args) {
        int n = 3;
        System.out.println("Steps to solve Tower of Hanoi for " + n + " disks:");
        solve(n, 'A', 'C', 'B');
    }
}
```

---

## 📌 Key Takeaway

The **Tower of Hanoi** elegantly demonstrates how:

* 🔁 **Recursion breaks a complex problem** into smaller sub-problems.
* 🧩 Each step is solved systematically until the **base case**.
* 📚 It’s a classic example of **divide and conquer** in action.

---

## ⏭️ Next Up: **Lesson 13 – Recursion with Backtracking (N-Queens, Sudoku Solver)**
