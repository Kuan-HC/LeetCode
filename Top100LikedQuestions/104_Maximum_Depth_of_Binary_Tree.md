# Maximum Depth of Binary Tree
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Example 1:
```
     3
   /  \
  9    2
 / \  / \
     1   7

Output: 3
```
### Example 2:
```
    1
   / \
      2

Output: 2
```
### Example 3:
```
    
   / \
      

Output: 0
```
[LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/)  


# 二叉樹的最大深度  
給定一個二叉樹，找出其最大深度。

二叉樹的深度為根節點到最遠葉子節點的最長路徑上的節點數。

說明: 葉子節點是指沒有子節點的節點。  

# Solution
## C

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

int maxDepth(struct TreeNode* root){
    if(root == NULL)
        return 0;
    else if ((root->left == NULL) && (root->right == NULL))
        return 1;
    
    int left = maxDepth(root->left);
    int right = maxDepth(root->right);
    
    return 1 + (left > right? left:right);
}
```

* Note:  

1. 使用遞歸recursion 時需特別注意邊界的情況，本題的邊界狀況即為  root = Null  以及 (root->left == NULL) && (root->right == NULL)

2. Misra C 中禁止使用recursion 及鍊表，猜想是因為新的資料一直在生成，使用recursion沒有辦法終止  
   如果是固定的資料，也不應該每次啟動時重新計算 
