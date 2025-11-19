
Practical: 7 - Design Doubly Linked List with Insertion, Deletion, Traversal, Search, and Reverse
```
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;
    Node(int val) {
        data = val;
        prev = next = nullptr;
    }
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;

public:
    DoublyLinkedList() {
        head = tail = nullptr;
        size = 0;
    }

    void create(int x) {
        Node* node = new Node(x);
        head = tail = node;
        size = 1;
    }

    void insertBeg(int x) {
        Node* node = new Node(x);
        node->next = head;
        if (head) head->prev = node;
        head = node;
        if (!tail) tail = node;
        size++;
    }

    void insertEnd(int x) {
        Node* node = new Node(x);
        if (!tail) {
            head = tail = node;
        } else {
            tail->next = node;
            node->prev = tail;
            tail = node;
        }
        size++;
    }

    void insertPos(int pos, int x) {
        if (pos == 1) {
            insertBeg(x);
            return;
        }
        if (pos == size + 1) {
            insertEnd(x);
            return;
        }
        Node* temp = head;
        for (int i = 1; i < pos - 1 && temp; i++) {
            temp = temp->next;
        }
        if (!temp) return; // invalid
        Node* node = new Node(x);
        node->next = temp->next;
        if (temp->next) temp->next->prev = node;
        temp->next = node;
        node->prev = temp;
        if (node->next == nullptr) tail = node;
        size++;
    }

    void deleteVal(int x) {
        Node* temp = head;
        while (temp && temp->data != x) {
            temp = temp->next;
        }
        if (!temp) {
            cout << -1 << "\n";
            return;
        }
        cout << temp->data << "\n";
        if (temp->prev) temp->prev->next = temp->next;
        else head = temp->next;
        if (temp->next) temp->next->prev = temp->prev;
        else tail = temp->prev;
        delete temp;
        size--;
    }

    void traverse() {
        Node* temp = head;
        while (temp) {
            cout << temp->data;
            if (temp->next) cout << " ";
            temp = temp->next;
        }
        cout << "\n";
    }

    void reverseTraverse() {
        Node* temp = tail;
        while (temp) {
            cout << temp->data;
            if (temp->prev) cout << " ";
            temp = temp->prev;
        }
        cout << "\n";
    }

    void search(int x) {
        Node* temp = head;
        int pos = 1;
        while (temp) {
            if (temp->data == x) {
                cout << pos << "\n";
                return;
            }
            temp = temp->next;
            pos++;
        }
        cout << -1 << "\n";
    }
};

int main() {
    int Q;
    cin >> Q;
    DoublyLinkedList dll;

    while (Q--) {
        string op;
        cin >> op;
        if (op == "create") {
            int x; cin >> x;
            dll.create(x);
        } else if (op == "insertBeg") {
            int x; cin >> x;
            dll.insertBeg(x);
        } else if (op == "insertEnd") {
            int x; cin >> x;
            dll.insertEnd(x);
        } else if (op == "insertPos") {
            int pos, x; cin >> pos >> x;
            dll.insertPos(pos, x);
        } else if (op == "delete") {
            int x; cin >> x;
            dll.deleteVal(x);
        } else if (op == "traverse") {
            dll.traverse();
        } else if (op == "search") {
            int x; cin >> x;
            dll.search(x);
        } else if (op == "reverse") {
            dll.reverseTraverse();
        }
    }
    return 0;
}
```
