# 面試金典 0404  檢查平衡性

實現一個函數，檢查二叉樹是否平衡。在這個問題中，平衡樹的定義如下：任意一個節點，其兩棵子樹的高度差不超過 1。

[LeetCode](https://leetcode-cn.com/problems/check-balance-lcci/)

### Example 1
```
給定二叉樹 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
返回 true 。
```

### Example 2
```
給定二叉樹 [1,2,2,3,3,null,null,4,4]
      1
     / \
    2   2
   / \
  3   3
 / \
4   4
返回 false 。
```

來源：力扣（LeetCode）
鏈接：https://leetcode-cn.com/problems/check-balance-lcci
著作權歸領扣網絡所有。商業轉載請聯系官方授權，非商業轉載請注明出處。

## Solution  

### C++

* 時間複雜度 O(n) 需遍曆所有的點

* 空間複雜度 O(n) 當最糟的情形，樹退化成鍊表時

```
#include <algorithm>

using namespace std;

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
    int DFS(TreeNode *root)
    {
        if (root == nullptr || ret == false)
            return 0;

        int left = DFS(root->left);
        int right = DFS(root->right);

        if (abs(left - right) > 1)
            ret = false;

        return max(left, right) + 1;
    }

public:
    bool isBalanced(TreeNode *root)
    {
        if (root == nullptr)
            return true;

        (void)DFS(root);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(0), B(1), C(2), D(3), E(4);
    A.left = &B;
    //A.right = &C;
    B.left = &D;
    C.left = &E;

    /* Test*/
    Solution test;
    bool ret = test.isBalanced(&A);

    return 0;
}
```