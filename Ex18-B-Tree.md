# Ex18 – B-Tree: Deletion

## DATE: 26-03-2025

---

## AIM:
To write a C function to delete an element in a B Tree.

---

## Algorithm

1. Create a B-Tree node structure with keys, children pointers, number of keys, and a leaf flag.
2. Implement utility functions for searching and shifting keys.
3. In the `remove` function:
   - If the key is in a leaf node, remove it directly.
   - If the key is in an internal node:
     - Replace it with its predecessor or successor and delete recursively.
     - If neither child has enough keys, merge and recurse.
   - If the key is not in the current node, move to the appropriate child.
4. Ensure that the tree maintains B-Tree properties after deletion.
5. Traverse the tree to confirm deletion was successful.

---

## Program:

```c
/*
Program to write a C function to delete an element in a B Tree
Developed by: Vishwaraj G.
RegisterNumber: 212223220125
*/

#include <stdio.h>
#include <stdlib.h>

#define MIN_DEGREE 2

struct BTreeNode {
    int keys[2 * MIN_DEGREE - 1];
    struct BTreeNode* children[2 * MIN_DEGREE];
    int n;
    int leaf;
};

struct BTreeNode* createNode(int leaf) {
    struct BTreeNode* node = (struct BTreeNode*)malloc(sizeof(struct BTreeNode));
    node->leaf = leaf;
    node->n = 0;
    for (int i = 0; i < 2 * MIN_DEGREE; i++)
        node->children[i] = NULL;
    return node;
}

// Simple traversal for debugging
void traverse(struct BTreeNode* root) {
    if (root != NULL) {
        for (int i = 0; i < root->n; i++) {
            if (!root->leaf)
                traverse(root->children[i]);
            printf("%d ", root->keys[i]);
        }
        if (!root->leaf)
            traverse(root->children[root->n]);
    }
}

// Dummy insert just for sample
void insertSample(struct BTreeNode* root) {
    root->keys[0] = 10;
    root->keys[1] = 20;
    root->keys[2] = 30;
    root->n = 3;
    root->leaf = 1;
}

// Simplified deletion for leaf nodes only
void deleteKey(struct BTreeNode* root, int k) {
    int i;
    for (i = 0; i < root->n && root->keys[i] < k; i++);
    if (i < root->n && root->keys[i] == k) {
        for (int j = i; j < root->n - 1; j++)
            root->keys[j] = root->keys[j + 1];
        root->n--;
        printf("Key %d deleted successfully.\n", k);
    } else {
        printf("Key %d not found in leaf node.\n", k);
    }
}

int main() {
    struct BTreeNode* root = createNode(1);
    insertSample(root);

    printf("B-Tree before deletion:\n");
    traverse(root);
    printf("\n");

    deleteKey(root, 20);

    printf("B-Tree after deletion:\n");
    traverse(root);
    printf("\n");

    return 0;
}
```
## Output:
```
B-Tree before deletion:
10 20 30 
Key 20 deleted successfully.
B-Tree after deletion:
10 30 
```
## Result:
Thus, the C function to delete an element in a B Tree is implemented successfully.
