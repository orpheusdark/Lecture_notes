
Practical: 1 - Implement Stack Operations

#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Stack {
private:
    int capacity;
    int top;
    vector<int> arr;

public:
    // Constructor with capacity
    Stack(int cap) {
        capacity = cap;
        top = -1;
        arr.resize(capacity);
    }

    // Push operation
    void push(int x) {
        if (top == capacity - 1) {
            cout << "Stack Overflow" << endl;
            return;
        }
        arr[++top] = x;
    }

    // Pop operation
    void pop() {
        if (top == -1) {
            cout << "Stack Underflow" << endl;
            return;
        }
        cout << arr[top--] << endl;
    }

    // Peek operation
    void peek() {
        if (top == -1) {
            cout << -1 << endl;
            return;
        }
        cout << arr[top] << endl;
    }

    // Traverse operation
    void traverse() {
        if (top == -1) {
            cout << "" << endl; // empty stack
            return;
        }
        for (int i = top; i >= 0; i--) {
            cout << arr[i];
            if (i != 0) cout << " ";
        }
        cout << endl;
    }

    // Search operation
    void search(int x) {
        for (int i = top; i >= 0; i--) {
            if (arr[i] == x) {
                cout << (top - i + 1) << endl; // 1-based position from top
                return;
            }
        }
        cout << -1 << endl;
    }
};

int main() {
    int Q;
    cin >> Q;

    Stack* st = nullptr; // initially no stack

    while (Q--) {
        string op;
        cin >> op;

        if (op == "create") {
            int cap;
            cin >> cap;
            st = new Stack(cap);
        } 
        else if (op == "push") {
            int x;
            cin >> x;
            st->push(x);
        } 
        else if (op == "pop") {
            st->pop();
        } 
        else if (op == "peek") {
            st->peek();
        } 
        else if (op == "traverse") {
            st->traverse();
        } 
        else if (op == "search") {
            int x;
            cin >> x;
            st->search(x);
        }
    }

    return 0;
}