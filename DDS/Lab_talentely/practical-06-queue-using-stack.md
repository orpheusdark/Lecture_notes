
Practical: 6 - Design Singly Linked List with Insertion, Deletion, Traversal, Search, and Reverse
```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(NULL) {}
};

class LinkedList {
    Node* head;

public:
    LinkedList() : head(NULL) {}

    // Insert at beginning
    void insertBeg(int x) {
        Node* newNode = new Node(x);
        newNode->next = head;
        head = newNode;
    }

    // Insert at end
    void insertEnd(int x) {
        Node* newNode = new Node(x);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }

    // Insert at position (1-based)
    void insertPos(int pos, int x) {
        if (pos <= 1 || !head) {
            insertBeg(x);
            return;
        }
        Node* newNode = new Node(x);
        Node* temp = head;
        for (int i = 1; i < pos - 1 && temp->next; i++) {
            temp = temp->next;
        }
        newNode->next = temp->next;
        temp->next = newNode;
    }

    // Delete by value
    void deleteVal(int x) {
        if (!head) {
            cout << "NOT FOUND\n";
            return;
        }
        if (head->data == x) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }
        Node* temp = head;
        while (temp->next && temp->next->data != x) {
            temp = temp->next;
        }
        if (!temp->next) {
            cout << "NOT FOUND\n";
            return;
        }
        Node* delNode = temp->next;
        temp->next = temp->next->next;
        delete delNode;
    }

    // Search
    void search(int x) {
        Node* temp = head;
        while (temp) {
            if (temp->data == x) {
                cout << "FOUND\n";
                return;
            }
            temp = temp->next;
        }
        cout << "NOT FOUND\n";
    }

    // Traverse
    void traverse() {
        if (!head) {
            cout << "EMPTY\n";
            return;
        }
        Node* temp = head;
        while (temp) {
            cout << temp->data;
            temp = temp->next;
            if (temp) cout << " ";
        }
        cout << "\n";
    }

    // Reverse list
    void reverse() {
        Node* prev = NULL;
        Node* curr = head;
        Node* next = NULL;
        while (curr) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        head = prev;
    }
};

int main() {
    int Q;
    cin >> Q;
    LinkedList list;

    while (Q--) {
        string op;
        cin >> op;
        if (op == "insertBeg") {
            int x; cin >> x;
            list.insertBeg(x);
        } 
        else if (op == "insertEnd") {
            int x; cin >> x;
            list.insertEnd(x);
        } 
        else if (op == "insertPos") {
            int p, x; cin >> p >> x;
            list.insertPos(p, x);
        } 
        else if (op == "delete") {
            int x; cin >> x;
            list.deleteVal(x);
        } 
        else if (op == "search") {
            int x; cin >> x;
            list.search(x);
        } 
        else if (op == "traverse") {
            list.traverse();
        } 
        else if (op == "reverse") {
            list.reverse();
        }
    }
    return 0;
}
```
