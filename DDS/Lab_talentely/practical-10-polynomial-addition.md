
practical: 10 -  Implement Binary search Tree and its operations ( creation, insertion, deletion).
```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) {
        data = val;
        left = right = nullptr;
    }
};

class BST {
public:
    Node* insert(Node* root, int val) {
        if (!root) return new Node(val);
        if (val < root->data)
            root->left = insert(root->left, val);
        else if (val > root->data)
            root->right = insert(root->right, val);
        return root;
    }

    Node* findMin(Node* root) {
        while (root && root->left)
            root = root->left;
        return root;
    }

    Node* deleteNode(Node* root, int val) {
        if (!root) return nullptr;
        if (val < root->data)
            root->left = deleteNode(root->left, val);
        else if (val > root->data)
            root->right = deleteNode(root->right, val);
        else {
            if (!root->left) {
                Node* temp = root->right;
                delete root;
                return temp;
            } else if (!root->right) {
                Node* temp = root->left;
                delete root;
                return temp;
            } else {
                Node* temp = findMin(root->right);
                root->data = temp->data;
                root->right = deleteNode(root->right, temp->data);
            }
        }
        return root;
    }

    void inorder(Node* root) {
        if (root) {
            inorder(root->left);
            cout << root->data << " ";
            inorder(root->right);
        }
    }
};

int main() {
    BST tree;
    Node* root = nullptr;
    int n, m, val;

    // Insert operations
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> val;
        root = tree.insert(root, val);
    }

    // Delete operations
    cin >> m;
    for (int i = 0; i < m; i++) {
        cin >> val;
        root = tree.deleteNode(root, val);
    }

    // Print final inorder
    if (!root) cout << "EMPTY";
    else tree.inorder(root);
    cout << endl;

    return 0;
}
```
