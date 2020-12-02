# Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).  
For example, this binary tree [1,2,2,3,4,4,3] is symmetric: 
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following [1,2,2,null,3,null,3] is not:  
```
  1
   / \
  2   2
   \   \
   3    3
```
[LeetCode](https://leetcode.com/problems/symmetric-tree/)  


# 對稱二叉樹  
給定一個二叉樹，檢查它是曾是鏡像對稱的  

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

bool helpler(struct TreeNode* l_root, struct TreeNode* r_root){
    if(l_root == NULL && r_root ==NULL)
        return true;
    else if(l_root == NULL || r_root ==NULL)
        return false;
    
    return (l_root->val == r_root->val) && helpler(l_root->left, r_root->right) && helpler(l_root->right,r_root->left); 
}

bool isSymmetric(struct TreeNode* root){
    if (root == NULL)
        return true;  

    return  helpler(root->left, root->right);
}
```

* Note:  

1. 使用遞歸recursion 時需特別注意邊界的情況，本題的邊界狀況即為 next = Null  

2. Misra C 中禁止使用recursion 及鍊表，猜想是因為新的資料一直在生成，使用recursion沒有辦法終止  
   如果是固定的資料，也不應該每次啟動時重新計算 
