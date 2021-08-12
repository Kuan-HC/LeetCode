# 面試金典 0408 首個共同祖先

設計並實現一個算法，找出二叉樹中某兩個節點的第一個共同祖先。不得將其他的節點存儲在另外的數據結構中。注意：這不一定是二叉搜索樹。

[LeetCode](https://leetcode-cn.com/problems/first-common-ancestor-lcci/)

```
例如，給定如下二叉樹: root = [3,5,1,6,2,0,8,null,null,7,4]

    3
   / \
  5   1
 / \ / \
6  2 0  8
  / \
 7   4
```

### Example 1
```
輸入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
輸出: 3
解釋: 節點 5 和節點 1 的最近公共祖先是節點 3。
```

### Example 2
```
輸入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
輸出: 5
解釋: 節點 5 和節點 4 的最近公共祖先是節點 5。因為根據定義最近公共祖先節點可以為節點本身。
```

* 所有節點的值都是唯一的。
* p、q 為不同節點且均存在於給定的二叉樹中。


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
    TreeNode *ret{nullptr};

    bool dfs(TreeNode *root, TreeNode *p, TreeNode *q)
    {
        if (root == nullptr || ret != nullptr)
            return false;

        bool leftFound = dfs(root->left, p, q);
        bool rightFound = dfs(root->right, p, q);
        bool currFound = (root == p || root == q);

        if ((leftFound == true && rightFound == true) || (currFound == true && (leftFound == true || rightFound == true)))
            ret = root;

        return leftFound || rightFound || currFound;
    }

public:
    TreeNode *lowestCommonAncestor(TreeNode *root, TreeNode *p, TreeNode *q)
    {
        if (root == nullptr)
            return nullptr;

        dfs(root, p, q);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(0), B(1), C(6), D(3), E(7);
    A.left = &B;
    A.right = &C;
    B.left = &D;

    /* Test*/
    Solution test;
    TreeNode *ret = test.lowestCommonAncestor(&A, &B, &D);

    return 0;
}
```