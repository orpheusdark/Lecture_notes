# 📘 Lesson 13: **Queue**


## 🚶‍♂️ What is a Queue?

A **Queue** is a fundamental linear data structure that follows the **FIFO** principle:
👉 *The first element added is the first to be removed.*

### 📌 Real-Life Examples

* 👥 A line of people waiting at a ticket counter.
* 🖨️ A print queue managing documents.
* ⚙️ Tasks in a CPU scheduler.

---

## 🧾 Basic Queue Terminology

* 🎯 **Front (or Head):** Points to the first element; where elements are removed.
* 🎯 **Rear (or Tail):** Points to the last element; where elements are added.
* ➕ **Enqueue:** Add an element to the rear.
* ➖ **Dequeue:** Remove an element from the front.

---

## 🔢 Array Representation of a Linear Queue

A simple queue uses an array with two pointers: `front` and `rear`.

📍 **Initialization:** `front = -1`, `rear = -1`

📌 **Conditions:**

* ❌ **Queue is Empty:** `front == -1` or `front > rear`
* 🚫 **Queue is Full:** `rear == MAX_SIZE - 1`

---

## ✅ Pros of Queues

* 🧾 **Fair Ordering (FIFO):** Items are processed in order.
* ⚡ **Efficient Operations:** Enqueue and Dequeue are O(1).
* 🧠 **Simple Logic:** Easy to understand.
* 🌍 **Widely Used:** In buffering, scheduling, etc.

## ❌ Cons of a Simple Linear Queue

* 🔍 **Limited Access:** Only front and rear accessible; searching is O(n).
* 🧱 **Wasted Space:** After dequeuing, unused space cannot be reclaimed.

---

## ⚙️ Operations of a Linear Queue (in C)

### 1️⃣ Enqueue (Insert)

```c
void enqueue(int value) {
    if (rear == SIZE - 1) {
        printf("Queue is full\n");
    } else {
        if (front == -1) front = 0;
        rear++;
        queue[rear] = value;
    }
}
```

### 2️⃣ Dequeue (Remove)

```c
void dequeue() {
    if (front == -1 || front > rear) {
        printf("Queue is empty\n");
    } else {
        front++;
    }
}
```

### 3️⃣ Peek (Front Element)

```c
int peek() {
    if (front == -1 || front > rear) {
        printf("Queue is empty\n");
        return -1;
    } else {
        return queue[front];
    }
}
```

---

## 🔄 Circular Queue – The Efficient Upgrade

A **Circular Queue** connects the rear of the array back to the front, forming a logical circle and solving memory waste.

💡 **Why Circular?**

* In a linear queue, `front` moves forward on each dequeue.
* Even if space at the front is free, new elements **cannot** be added once `rear` hits the end.
* Circular queues **reuse this space efficiently**.

---

## 📊 Array Implementation of a Circular Queue

* Uses modulo `%` to wrap indices around.
* 🔹 **Increment Rear:** `rear = (rear + 1) % SIZE`
* 🔹 **Increment Front:** `front = (front + 1) % SIZE`

📌 **Conditions:**

* ❌ **Queue is Empty:** `front == -1`
* 🚫 **Queue is Full:** `(rear + 1) % SIZE == front`

---

## 🔧 Circular Queue Code (in C)

### ➕ Enqueue

```c
void enqueue(int value) {
    if ((rear + 1) % SIZE == front) {
        printf("Queue is full\n");
    } else {
        if (front == -1) front = 0;
        rear = (rear + 1) % SIZE;
        queue[rear] = value;
    }
}
```

### ➖ Dequeue

```c
void dequeue() {
    if (front == -1) {
        printf("Queue is empty\n");
    } else {
        if (front == rear) {
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % SIZE;
        }
    }
}
```

---

## 💪 Advantages of Circular Queue

* ♻️ **Efficient Memory Use:** No wasted space.
* ⚡ **Constant Time Operations:** O(1) enqueue and dequeue.
* 🖥️ **Perfect for Buffers:** Ideal for fixed-size buffer systems.

---

## ⏭️ Next: **Lesson 14 – Deque & Priority Queue**

