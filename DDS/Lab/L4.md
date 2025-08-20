# **🧠 LAB 4: Towers of Hanoi using Stacks (Recursive & Iterative Approaches)**




## **📜 1. Introduction**

The **Tower of Hanoi** puzzle is more than just a game — it’s a fundamental problem in **computer science**, especially for teaching **recursion, algorithm design, and stack usage**.

According to legend, ancient priests in a temple were tasked with moving **64 golden disks** from one peg to another, obeying strict divine rules. The prophecy claimed that when the priests finished, the world would end. 💀

But don’t worry — the number of moves required is **2⁶⁴ − 1 = 18,446,744,073,709,551,615**. Even at one move per second, that’s **584 billion years**! This highlights the **exponential time complexity O(2ⁿ)** of the problem.

In this lab, we’ll learn to solve the puzzle both **recursively** (using the call stack) and **iteratively** (using explicit stacks).

---

## **⚖️ 2. Problem Definition & Rules**

The puzzle involves **3 pegs** and `n` disks of different sizes. The disks start stacked on one peg in decreasing size order (largest at bottom, smallest at top).

* **🎯 Goal:** Move all `n` disks from the **Source (A)** peg to the **Destination (C)** peg, using **Auxiliary (B)** peg for help.
* **📜 Rules:**

  1. You may move **only one disk at a time**.
  2. No **larger disk may be placed on a smaller disk**.

**Example for n=3 (Initial & Final States):**

```
Initial:    A: [3,2,1]   B: []   C: []
Goal:       A: []        B: []   C: [3,2,1]
```

---

## **🧠 3. Recursive Solution (Elegant Divide-and-Conquer)**

The recursive approach is natural because the problem can be **redefined in smaller sub-problems**.

### **🚀 Recursive Insight**

* **Base Case (n=1):** Move disk directly from A → C. ✅
* **Recursive Case (n>1):**

  1. Move `n−1` disks from A → B (using C as helper).
  2. Move the largest disk from A → C.
  3. Move the `n−1` disks from B → C (using A as helper).

Each step obeys the rules, and recursion handles the sub-problems until the base case is reached.

---

### **💻 Recursive C++ Implementation**

```cpp
#include <iostream>
using namespace std;

// n: number of disks
// source: starting peg
// destination: target peg
// auxiliary: helper peg
void hanoi(int n, char source, char destination, char auxiliary) {
    // Base Case: If only one disk, move it and stop.
    if (n == 1) {
        cout << "➡️ Move disk 1 from " << source << " to " << destination << endl;
        return;
    }
    
    // Recursive Case:
    // Step 1: Move n-1 disks from source to auxiliary (using destination as temp)
    hanoi(n - 1, source, auxiliary, destination);
    
    // Step 2: Move the nth disk from source to destination
    cout << "➡️ Move disk " << n << " from " << source << " to " << destination << endl;
    
    // Step 3: Move n-1 disks from auxiliary to destination (using source as temp)
    hanoi(n - 1, auxiliary, destination, source);
}

int main() {
    int n = 3;
    cout << "🧪 Tower of Hanoi (Recursive C++) - Steps for " << n << " disks:" << endl << endl;
    hanoi(n, 'A', 'C', 'B'); // Move from A to C using B
    return 0;
}
```

**Sample Output (n=3):**

```
➡️ Move disk 1 from A to C
➡️ Move disk 2 from A to B
➡️ Move disk 1 from C to B
➡️ Move disk 3 from A to C
➡️ Move disk 1 from B to A
➡️ Move disk 2 from B to C
➡️ Move disk 1 from A to C
```

---

## **🔄 4. Iterative Solution (Explicit Stack Simulation)**

Recursion uses the program’s **call stack**, but we can simulate it manually with stacks.

### **🧭 Iterative Insight**

* The solution requires **2ⁿ − 1 moves**.
* For **odd n**: moves follow the cycle → `(A→C, A→B, B→C)`
* For **even n**: moves follow the cycle → `(A→B, A→C, B→C)`
* At each step, always make the **legal move** between the two chosen pegs.

---

### **💻 Iterative Python Implementation**

```python
INT_MIN = float('-inf')

class Stack:
    def __init__(self):
        self.items = []
    def push(self, val):
        self.items.append(val)
    def pop(self):
        return self.items.pop() if not self.is_empty() else INT_MIN
    def top(self):
        return self.items[-1] if not self.is_empty() else INT_MIN
    def is_empty(self):
        return len(self.items) == 0

def move_disk(src, dest, s_name, d_name):
    # Check which move is legal: from src->dest or dest->src?
    if src.is_empty():
        # If source is empty, we must move FROM destination TO source
        disk = dest.pop()
        src.push(disk)
        print(f"➡️ Move disk {disk} from {d_name} to {s_name}")
    elif dest.is_empty():
        # If destination is empty, move FROM source TO destination
        disk = src.pop()
        dest.push(disk)
        print(f"➡️ Move disk {disk} from {s_name} to {d_name}")
    elif src.top() > dest.top():
        # If src's top is larger, it can't go on dest. Reverse the move.
        disk = dest.pop()
        src.push(disk)
        print(f"➡️ Move disk {disk} from {d_name} to {s_name}")
    else:
        # Legal move: src.top < dest.top, so move it.
        disk = src.pop()
        dest.push(disk)
        print(f"➡️ Move disk {disk} from {s_name} to {d_name}")

def towers_of_hanoi(n):
    src, aux, dest = Stack(), Stack(), Stack()
    s, a, d = 'A', 'B', 'C'

    # Key Insight: For even n, the cycle changes by swapping B and C.
    if n % 2 == 0:
        a, d = d, a  # Swap the roles of auxiliary and destination

    # Initialize source stack with disks (largest at bottom)
    for disk_size in range(n, 0, -1):
        src.push(disk_size)

    total_moves = (1 << n) - 1  # This is 2^n - 1

    for move_number in range(1, total_moves + 1):
        if move_number % 3 == 1:
            move_disk(src, dest, s, d) # Check between A and C
        elif move_number % 3 == 2:
            move_disk(src, aux, s, a) # Check between A and B
        else: # move_number % 3 == 0
            move_disk(aux, dest, a, d) # Check between B and C

# Run the program
n = int(input("Enter number of disks: "))
towers_of_hanoi(n)
```

**Output (n=3):**

```
➡️ Move disk 1 from A to C
➡️ Move disk 2 from A to B
➡️ Move disk 1 from C to B
➡️ Move disk 3 from A to C
➡️ Move disk 1 from B to A
➡️ Move disk 2 from B to C
➡️ Move disk 1 from A to C
```

---

## **📊 5. Recursive vs Iterative Approaches**

| Feature              | Recursive                                | Iterative                |
| -------------------- | ---------------------------------------- | ------------------------ |
| **Concept**          | Divide & conquer                         | Pattern-based simulation |
| **Data Structure**   | Call stack                               | Explicit stack objects   |
| **Ease of Use**      | Intuitive (once recursion is understood) | Less intuitive           |
| **Control**          | Compiler handles function calls          | Programmer manages stack |
| **Space Complexity** | O(n) (stack frames)                      | O(n) (3 stacks)          |
| **Time Complexity**  | O(2ⁿ)                                    | O(2ⁿ)                    |

✅ Both solutions are correct. The recursive one is elegant, while the iterative one proves that **recursion can always be converted to iteration** with explicit stacks.

---

## **❓ Viva Questions**

**Q1:** What is recursion?

**A1:** A programming technique where a function calls itself on smaller sub-problems until a base case is reached.



**Q2:** What is the base case in Hanoi recursion?

**A2:** When `n == 1`, directly move the disk.



**Q3:** What is the recurrence relation for Hanoi?

**A3:** `T(n) = 2T(n-1) + 1`, solved as `T(n) = 2ⁿ − 1`.



**Q4:** What is the time complexity?

**A4:** **O(2ⁿ)** (exponential).



**Q5:** What data structure supports recursion?

**A5:** The **stack** (function call stack).


**Q6:** Can it be solved without stacks?

**A6:** Yes, using mathematical formulas or binary representation of moves, but stack-based solutions are the most intuitive.

