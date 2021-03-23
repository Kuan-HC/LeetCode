# 098. Validate Binary Search Tree

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

[LeetCode](https://leetcode.com/problems/validate-binary-search-tree)  

### Example 1:
<img src="img/098_q1.jpg" width = "300"/>

```
Input: root = [2,1,3]
Output: true
```
### Example 2:
<img src="img/098_q2.jpg" width = "300"/>

```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

#  驗證二叉搜索樹
給定一個二叉樹，判斷其是否是一個有效的二叉搜索樹。

假設一個二叉搜索樹具有如下特征：

節點的左子樹只包含小於當前節點的數。
節點的右子樹只包含大於當前節點的數。
所有左子樹和右子樹自身必須也是二叉搜索樹

## Solution
* DFS
* 使用上下範圍，目的是為了在當前node，處理完該點數字的驗證


### C

```
/* Definition for a binary tree node. */
struct TreeNode
{
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

bool DFS(struct TreeNode *root, long low, long high)
{
    bool ret = true;

    if (root == NULL)
        return true;

    int num = root->val;

    if( num <= low || num>= high)
        return false;

    return  DFS(root->left, low, num) && DFS(root->right, num, high);

}

bool isValidBST(struct TreeNode *root)
{
    bool ret;
    ret = DFS(root, LONG_MIN, LONG_MAX);

    return ret;
}

int main()
{
    struct TreeNode A, B, C;
    A.left = NULL;
    A.right = NULL;
    A.val = 2;
    B.left = NULL;
    B.right = NULL;
    B.val = 4;
    C.left = NULL;
    C.right = NULL;
    C.val = 3;

    bool ans = isValidBST(&A);

    return 0;
}
```
