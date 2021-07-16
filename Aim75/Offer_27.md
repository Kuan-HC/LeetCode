# 劍指 Offer 27 二叉樹的鏡像

請完成一個函數，輸入一個二叉樹，該函樹輸出它的鏡像
 
[LeetCode](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)


### Example 1
* Input
```
      4
   /   \
  2     7
 / \   / \
1   3 6   9
```
* Output*

```
      4
   /   \
  7     2
 / \   / \
9   6 3   1
```


* 0 <= 節點數 <= 1000

## Solution  


### C++

* 時間複雜度: O(n) 

* 空間複雜度: O(n) 


```
/* Definition for singly-linked list. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution
{
public:
    TreeNode *mirrorTree(TreeNode *root)
    {
        /* Recursion stop condition*/
        if(root == nullptr)
            return nullptr;

        TreeNode* tmp = root->left;

        root->left = root->right;
        root->right = tmp;

        /* go deeper to next level branch*/
        mirrorTree(root -> left);
        mirrorTree(root -> right);

        return root;
    }
};

int main()
{
    /* input*/
    TreeNode A(3), B(4), C(5), D(1), E(2);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    B.right = &E;

    /* Test*/
    Solution test;
    TreeNode* res = test.mirrorTree(&A);

    return 0;
}
```