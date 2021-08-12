# 面試金典 0406  後繼者

設計一個算法，找出二叉搜索樹中指定節點的“下一個”節點（也即中序後繼）。

如果指定節點沒有對應的“下一個”節點，則返回null。

[LeetCode](https://leetcode-cn.com/problems/successor-lcci/)

### Example 1
```
輸入: root = [2,1,3], p = 1

  2
 / \
1   3

輸出: 2
```


### Example 2
```
輸入: root = [5,3,6,2,4,null,null,1], p = 6

      5
     / \
    3   6
   / \
  2   4
 /   
1

輸出: null
```

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
    bool found{false};
    TreeNode *ret{nullptr};

    void dfs(TreeNode *root, TreeNode *p)
    {
        if (root == nullptr || ret != nullptr)
            return;

        /* left branch*/
        dfs(root->left, p);
        /* process inorder*/
        if (found == true && ret ==nullptr)
        {
            ret = root;
            return;
        }

        if (root == p)
            found = true;

        /* right branch*/
        dfs(root->right, p);
    }

public:
    TreeNode *inorderSuccessor(TreeNode *root, TreeNode *p)
    {
        if (root == nullptr)
            return nullptr;

        dfs(root, p);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(0), B(1), C(6), D(3), E(7);
    A.left = &B;
    A.right = &C;
    

    /* Test*/
    Solution test;
    TreeNode *ret = test.inorderSuccessor(&A, &B);

    return 0;
}
```