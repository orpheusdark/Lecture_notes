
Practical: 11 - Implement Traversals Preorder Inorder Postorder on BST.
```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

// Insert into BST
Node* insert(Node* root, int val) {
    if (root == NULL) return new Node(val);
    if (val < root->data)
        root->left = insert(root->left, val);
    else
        root->right = insert(root->right, val);
    return root;
}

// Preorder Traversal (Root, Left, Right)
void preorder(Node* root) {
    if (root == NULL) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Inorder Traversal (Left, Root, Right)
void inorder(Node* root) {
    if (root == NULL) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Postorder Traversal (Left, Right, Root)
void postorder(Node* root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

int main() {
    int n;
    cin >> n;
    Node* root = NULL;
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        root = insert(root, x);
    }

    // Print Traversals
    preorder(root);
    cout << endl;
    inorder(root);
    cout << endl;
    postorder(root);
    cout << endl;

    return 0;
}
```
