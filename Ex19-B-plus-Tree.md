# Ex19 – B+ Tree Traversal

## DATE: 27-03-2025

---

## AIM:
To write a C function to traverse the elements in a B+ Tree.

---

## Algorithm

1. Define the structure of a B+ Tree node including keys, child pointers, and leaf flag.
2. Create functions for inserting values and linking leaf nodes for traversal.
3. To traverse, start from the leftmost leaf and follow the linked list of leaves.
4. At each leaf node, print all key values.
5. Continue until the last leaf node is reached.

---

## Program:

```c
/*
Program to traverse the elements in a B+ Tree.
Developed by: Vishwaraj G.
RegisterNumber: 212223220125
*/

#include <stdio.h>
#include <stdlib.h>

#define MAX 3

typedef struct BPlusNode {
    int leaf;
    int n;
    int keys[MAX];
    struct BPlusNode* children[MAX + 1];
    struct BPlusNode* next; // for leaf node linking
} BPlusNode;

// Create a new B+ Tree node
BPlusNode* createNode(int leaf) {
    BPlusNode* node = (BPlusNode*)malloc(sizeof(BPlusNode));
    node->leaf = leaf;
    node->n = 0;
    node->next = NULL;
    for (int i = 0; i < MAX + 1; i++)
        node->children[i] = NULL;
    return node;
}

// Sample insert directly into leaf (for demo purposes)
void insertSample(BPlusNode* root) {
    root->keys[0] = 5;
    root->keys[1] = 15;
    root->keys[2] = 25;
    root->n = 3;
    root->leaf = 1;

    BPlusNode* nextLeaf = createNode(1);
    nextLeaf->keys[0] = 35;
    nextLeaf->keys[1] = 45;
    nextLeaf->n = 2;
    root->next = nextLeaf;
}

// Traverse B+ Tree (leaf level)
void traverse(BPlusNode* root) {
    BPlusNode* temp = root;
    while (temp != NULL) {
        for (int i = 0; i < temp->n; i++) {
            printf("%d ", temp->keys[i]);
        }
        temp = temp->next;
    }
    printf("\n");
}

int main() {
    BPlusNode* root = createNode(1);
    insertSample(root);

    printf("B+ Tree Traversal (Leaf Level):\n");
    traverse(root);

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
