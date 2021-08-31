# 105. Construct Binary Tree from Preorder and Inorder Traversal

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

[LeetCode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)  

### Example 1:
<img src="img/105_q.jpg" width = "300"/>

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

### Example 2:
```
Input: root = [1]
Output: [[1]]
```

### Example 2:
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

#  從前序與中序遍歷序列構造二叉樹
根據一棵樹的前序遍歷與中序遍歷構造二叉樹。

注意:
你可以假設樹中沒有重覆的元素。

## Solution
* Depth-First Search

### C

```
/* Definition for a binary tree node.*/
struct TreeNode
{
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

struct TreeNode *buildTree(int *preorder, int preorderSize, int *inorder, int inorderSize)
{
    /* create a node to reture */
    struct TreeNode *ret = (struct TreeNode *)calloc(1, sizeof(struct TreeNode));
    ret->val = preorder[0];

    /* search preorder[0] position in inorder*/
    int i = 0;
    for (i = 0; i < inorderSize; ++i)
    {
        if (inorder[i] == preorder[0])
            break;
    }
    /**
     *  we have i, now can divide inorder to left and right group
     *  Declared following variables so it is easier to understand
     * */

    /*left group*/
    int leftInOrderSize = i;
    int *leftInOrder = inorder;
    int *leftPreOrder = preorder + 1;
    if (leftInOrderSize != 0)
        ret->left = buildTree(leftPreOrder, leftInOrderSize, leftInOrder, leftInOrderSize);

    /* right group*/
    int rightInOrderSize = inorderSize - i - 1;
    int *rightInOrder = inorder + i + 1;
    int *rightPreOrder = preorder + 1 + leftInOrderSize;
    if (rightInOrderSize != 0)
        ret->right = buildTree(rightPreOrder, rightInOrderSize, rightInOrder, rightInOrderSize);

    return ret;
}

int main()
{
    int preorder[] = {3, 9, 20, 15, 7};
    int inorder[] = {9, 3, 15, 20, 7};

    struct TreeNode *ans = buildTree(preorder, sizeof(preorder) / sizeof(preorder[0]), inorder, sizeof(inorder) / sizeof(inorder[0]));

    return 0;
}
```
