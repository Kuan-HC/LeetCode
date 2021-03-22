# 094. Binary Tree Inorder Traversal

Given the root of a binary tree, return the inorder traversal of its nodes' values.

[LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal)  

### Example 1:
<img src="img/094_q.jpg" width = "250"/>
```
Input: root = [1,null,2,3]
Output: [1,3,2]
```

### Example 2:
```
Input: root = []
Output: []
```

### Example 3:
```
Input: root = [1]
Output: [1]
```

#  二叉樹的中序遍歷
給定一個二叉樹的根節點 root，反回它的中序遍曆

## Solution
* Dpeth First Search

### C

```
/**
 * Definition for a binary tree node.
*/
struct TreeNode
{
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
void DFS(struct TreeNode *root, int *returnSize, int *retArray)
{
    if (root == NULL)
        return;

    DFS(root->left, returnSize, retArray);
    retArray[*returnSize] = root->val;
    ++*returnSize;
    DFS(root->right, returnSize, retArray);
}

int *inorderTraversal(struct TreeNode *root, int *returnSize)
{
    int *res = (int *)calloc(100, sizeof(int));
    *returnSize = 0;

    DFS(root, returnSize, res);

    return res;
}

int main()
{
    /* input */
    struct TreeNode A, B, C, D, E, F;
    A.val = 1;
    A.left = &B;
    A.right = &C;
    B.val = 2;
    B.left = &D;
    B.right = &E;
    C.val = 3;
    C.left = &F;
    C.right = NULL;
    D.val = 4;
    D.left = NULL;
    D.right = NULL;
    E.val = 5;
    E.left = NULL;
    E.right = NULL;
    F.val = 6;
    F.left = NULL;
    F.right = NULL;

    int returnSize = 0;

    /* algorithm */
    int *ans = inorderTraversal(&A, &returnSize);
    /* print answer */
    for (int i = 0; i < returnSize; ++i)
        printf("%2i, ", ans[i]);

        return 0;
}
```
