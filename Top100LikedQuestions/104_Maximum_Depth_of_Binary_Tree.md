# 104. Maximum Depth of Binary Tree
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## 二叉樹的最大深度  
給定一個二叉樹，找出其最大深度。

二叉樹的深度為根節點到最遠葉子節點的最長路徑上的節點數。

說明: 葉子節點是指沒有子節點的節點。

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

## Solution
### C++

```
#include <algorithm>

using namespace std;

/*  Definition for a binary tree node. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution {
public:

    int maxDepth(TreeNode* root) {

        if (root == nullptr)
            return 0;
        
        /* left branch*/
        int leftDepth = maxDepth(root->left);
        /* right branch*/
        int rightDepth = maxDepth(root->right);

        return max(leftDepth, rightDepth) + 1;
    }
};

int main()
{
    /* Input*/
    TreeNode A(1), B(2), C(3), D(4), E(5), F(6), G(7);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    B.right = &G;
    C.left = &E;
    C.right = &F;

    /* unit test*/
    Solution test;
    int res = test.maxDepth(&A);

    int test1 = 7 % 2;
    int test2 = 7 & (2 - 1);

    return 0;
}
```

* Note:  

1. 使用遞歸recursion 時需特別注意邊界的情況，本題的邊界狀況即為  root = Null  以及 (root->left == NULL) && (root->right == NULL)

2. Misra C 中禁止使用recursion 及鍊表，猜想是因為新的資料一直在生成，使用recursion沒有辦法終止  
   如果是固定的資料，也不應該每次啟動時重新計算 
ㄒ