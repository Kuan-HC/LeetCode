# 114. Flatten Binary Tree to Linked List

Given the root of a binary tree, flatten the tree into a "linked list":

The "linked list" should use the same TreeNode class where the right child pointer points to the next node in the list and the left child pointer is always null.
The "linked list" should be in the same order as a pre-order traversal of the binary tree.

[LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)  

### Example 1:
<img src="img/114_q.jpg" width = "500"/>

```
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
```

### Example 2:
```
Input: root = []
Output: []
```

### Example 3:
```
Input: root = [0]
Output: [0]
```

#  二叉樹展開為鍊表
給你二叉樹的根結點 root ，請你將它展開為一個單鏈表：

展開後的單鏈表應該同樣使用 TreeNode ，其中 right 子指針指向鏈表中下一個結點，而左子指針始終為 null 。
展開後的單鏈表應該與二叉樹 先序遍歷 順序相同。

## Solution
* Depth-First Search
* First. reat a list to store the preorder sequence
* Reconnect the nodes

### C

```
/* Definition for a binary tree node.*/
struct TreeNode
{
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

#define MAX_Len 2000

void DFS(struct TreeNode *root, struct TreeNode **queue, int *index)
{
    if (root == NULL)
        return;

    /* record node info into queue*/
    queue[*index] = root;
    ++*index;
    /* left branch*/
    DFS(root->left, queue, index);
    /* right branch*/
    DFS(root->right, queue, index);
}



void flatten(struct TreeNode *root)
{
    /*record the preorder sequence*/
    int index = 0;
    struct TreeNode **queue = (struct TreeNode **)calloc(MAX_Len, sizeof(struct TreeNode *));
    DFS(root, queue, &index);

    for (int i = 0; i < index - 1; ++i)
    {
        struct TreeNode* tmp = queue[i];  /* for debug*/
        tmp->left = NULL;
        tmp->right = queue[i+1];        
    }

}

int main()
{

    /* input */
    struct TreeNode A, B, C, D, E;
    A.val = 1;
    A.left = &B;
    A.right = &C;

    B.val = 2;
    B.left = &D;
    B.right = NULL;

    C.val = 3;
    C.left = NULL;
    C.right = &E;

    D.val = 4;
    D.right = NULL;
    D.left = NULL;

    E.val = 5;
    E.left = NULL;
    E.right = NULL;

    /* Algorithm */
    flatten(&A);

    return 0;
}
```
