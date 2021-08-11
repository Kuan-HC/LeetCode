# 面試金典 0405  合法二叉搜索樹

實現一個函數，檢查一棵二叉樹是否為二叉搜索樹。

[LeetCode](https://leetcode-cn.com/problems/legal-binary-search-tree-lcci/)

### Example 1
```
輸入:
    2
   / \
  1   3
輸出: true
示例 2:
輸入:
    5
   / \
  1   4
     / \
    3   6
輸出: false
解釋: 輸入為: [5,1,4,null,null,3,6]。
     根節點的值為 5 ，但是其右子節點值為 4 。
```



## Solution  

### C++

* 時間複雜度 O(n) 需遍曆所有的點

* 空間複雜度 O(n) 當最糟的情形，樹退化成鍊表時

```
/* Definition for a binary tree node. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution
{
private:
    bool ret{true};

    void dfs(TreeNode *root,  long left, long right)
    {
        if (root == nullptr || ret == false)
            return;

        if (root->val <= left || root->val >= right)
            ret = false;

        /*left branch*/
        dfs(root->left, left, root->val);
        /* right branch*/
        dfs(root->right, root->val, right);        
    }

    

public:
    bool isValidBST(TreeNode *root)
    {
        if (root == nullptr)
            return true;

        dfs(root, LONG_MIN, LONG_MAX);
        
        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(2147483647), B(1), C(6), D(3), E(7);
    A.left = &B;
    A.right = &C;
    C.left = &D;
    C.right = &E;

    /* Test*/
    Solution test;
    bool ret = test.isValidBST(&A);

    return 0;
}
```