Practical: 5 - Design Queue with Enqueue, Dequeue, Traverse, and Search
```
#include <iostream>
using namespace std;

#define MAX 100   // max queue size

class Queue {
    int arr[MAX];
    int front, rear;

public:
    Queue() {
        front = 0;
        rear = -1;
    }

    bool isEmpty() {
        return (rear < front);
    }

    bool isFull() {
        return (rear == MAX - 1);
    }

    void enqueue(int x) {
        if (isFull()) return; // ignore if full
        arr[++rear] = x;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "EMPTY\n";
        } else {
            cout << arr[front++] << "\n";
        }
    }

    void traverse() {
        if (isEmpty()) {
            cout << "EMPTY\n";
            return;
        }
        for (int i = front; i <= rear; i++) {
            cout << arr[i];
            if (i < rear) cout << " ";
        }
        cout << "\n";
    }

    void search(int x) {
        for (int i = front; i <= rear; i++) {
            if (arr[i] == x) {
                cout << "FOUND\n";
                return;
            }
        }
        cout << "NOT FOUND\n";
    }
};

int main() {
    int Q;
    cin >> Q;
    Queue q;

    while (Q--) {
        string op;
        cin >> op;
        if (op == "enqueue") {
            int x; cin >> x;
            q.enqueue(x);
        } 
        else if (op == "dequeue") {
            q.dequeue();
        } 
        else if (op == "traverse") {
            q.traverse();
        } 
        else if (op == "search") {
            int x; cin >> x;
            q.search(x);
        }
    }
    return 0;
}
```
