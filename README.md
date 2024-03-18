# 10thDevelop a menu driven Program in C for the following operations on Binary Search Tree (BST) 
of Integers . a. Create a BST of N Integers: 6, 9, 5, 2, 8, 15, 24, 14, 7, 8, 5, 2 b. Traverse the BST in 
Inorder, Preorder and Post Order c. Search the BST for a given element (KEY) and report the 
appropriate message d. Exit.

#include <stdio.h>
#include <stdlib.h>

// Structure to represent a node in the binary search tree
struct TreeNode {
    int data;
    struct TreeNode *left;
    struct TreeNode *right;
};

// Function prototypes
struct TreeNode* createNode(int value);
struct TreeNode* insertNode(struct TreeNode *root, int value);
void inorderTraversal(struct TreeNode *root);
void preorderTraversal(struct TreeNode *root);
void postorderTraversal(struct TreeNode *root);
struct TreeNode* search(struct TreeNode *root, int key);

int main() {
    struct TreeNode *root = NULL;
    int choice, value, key;
    
    // Create the initial BST
    int initialData[] = {6, 9, 5, 2, 8, 15, 24, 14, 7, 8, 5, 2};
    int numInitialData = sizeof(initialData) / sizeof(initialData[0]);
    for (int i = 0; i < numInitialData; i++) {
        root = insertNode(root, initialData[i]);
    }

    do {
        printf("\nBinary Search Tree Operations Menu:\n");
        printf("a. Traverse the BST in Inorder\n");
        printf("b. Traverse the BST in Preorder\n");
        printf("c. Traverse the BST in Postorder\n");
        printf("d. Search the BST for a given element (KEY)\n");
        printf("e. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);

        switch (choice) {
            case 'a':
                printf("Inorder Traversal: ");
                inorderTraversal(root);
                printf("\n");
                break;

            case 'b':
                printf("Preorder Traversal: ");
                preorderTraversal(root);
                printf("\n");
                break;

            case 'c':
                printf("Postorder Traversal: ");
                postorderTraversal(root);
                printf("\n");
                break;

            case 'd':
                printf("Enter the element to search: ");
                scanf("%d", &key);
                struct TreeNode *result = search(root, key);
                if (result != NULL) {
                    printf("Element %d found in the BST.\n", key);
                } else {
                    printf("Element %d not found in the BST.\n", key);
                }
                break;

            case 'e':
                printf("Exiting program.\n");
                break;

            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    } while (choice != 'e');

    return 0;
}

// Function to create a new node with the given value
struct TreeNode* createNode(int value) {
    struct TreeNode *newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    if (newNode == NULL) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a node with the given value into the BST
struct TreeNode* insertNode(struct TreeNode *root, int value) {
    if (root == NULL) {
        root = createNode(value);
    } else if (value < root->data) {
        root->left = insertNode(root->left, value);
    } else if (value > root->data) {
        root->right = insertNode(root->right, value);
    }
    return root;
}

// Function to perform inorder traversal of the BST
void inorderTraversal(struct TreeNode *root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->data);
        inorderTraversal(root->right);
    }
}

// Function to perform preorder traversal of the BST
void preorderTraversal(struct TreeNode *root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

// Function to perform postorder traversal of the BST
void postorderTraversal(struct TreeNode *root) {
    if (root != NULL) {
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        printf("%d ", root->data);
    }
}

// Function to search for a given key in the BST
struct TreeNode* search(struct TreeNode *root, int key) {
    if (root == NULL || root->data == key) {
        return root;
    }
    if (key < root->data) {
        return search(root->left, key);
    }
    return search(root->right, key);
}
