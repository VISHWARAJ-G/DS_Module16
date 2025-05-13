# Ex17 – AVL Tree: Right Rotation

## DATE: 25-03-2025

---

## AIM:
To write a C function to perform right rotation in an AVL Tree.

---

## Algorithm

1. Create an AVL node structure with data, left and right children, and height.
2. Define a `rightRotate` function that:
   - Takes a node `y` as input.
   - Sets `x = y->left` and `T2 = x->right`.
   - Performs the right rotation by making `x` the new root, `y` as `x`'s right child, and `T2` as `y`'s left child.
   - Updates the heights of `y` and `x`.
   - Returns `x` (the new root after rotation).
3. Implement a simple AVL insert function for testing the rotation.
4. Call the rightRotate function when the tree becomes unbalanced due to left-heavy insertions.
5. Print the tree in-order to verify the correctness of rotation.

---

## Program:

```c
/*
Program to perform right rotation in AVL Tree
Developed by: Vishwaraj G.
RegisterNumber: 212223220125
*/

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
    int height;
};

int max(int a, int b) {
    return (a > b) ? a : b;
}

int getHeight(struct Node* node) {
    if (node == NULL)
        return 0;
    return node->height;
}

struct Node* createNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

struct Node* rightRotate(struct Node* y) {
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(getHeight(y->left), getHeight(y->right)) + 1;
    x->height = max(getHeight(x->left), getHeight(x->right)) + 1;

    return x;
}

void inOrder(struct Node* root) {
    if (root != NULL) {
        inOrder(root->left);
        printf("%d ", root->data);
        inOrder(root->right);
    }
}

// Test Right Rotation
int main() {
    struct Node* root = createNode(30);
    root->left = createNode(20);
    root->left->left = createNode(10);

    printf("Before Right Rotation (In-order):\n");
    inOrder(root);
    printf("\n");

    root = rightRotate(root);

    printf("After Right Rotation (In-order):\n");
    inOrder(root);
    printf("\n");

    return 0;
}
```
## Output:
```
Before Right Rotation (In-order):
10 20 30 
After Right Rotation (In-order):
10 20 30 
```
## Result:
Thus, the function to perform right rotation in an AVL Tree is implemented successfully.
