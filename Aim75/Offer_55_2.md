# 劍指 Offer 55-2 平衡二叉樹

輸入一棵二叉樹的根節點，判斷該樹是不是平衡二叉樹。如果某二叉樹中任意節點的左右子樹的深度相差不超過1，那麽它就是一棵平衡二叉樹。

[LeetCode](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

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

* 0 <= 樹的結點個數 <= 10000

## Solution  

### C++

* 時間複雜度：O(n) n 為二叉樹的深度

* 空間複雜度：O(n) 

```
/*  Definition for a binary tree node. */
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
    bool balance{true};

    int DFS(TreeNode *root)
    {
        if (root == nullptr || balance == false)
            return 0;

        /*left branch*/
        int leftDepth = DFS(root->left);
        int rightDepth = DFS(root->right);

        if (abs(leftDepth - rightDepth) > 1)
            balance = false;

        return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
    }

public:
    bool isBalanced(TreeNode *root)
    {
        static_cast<void>(DFS(root));

        return balance;
    }
};

int main()
{
    /* input*/
    TreeNode A(3), B(1), C(4);
    A.left = &B;
    A.right = &C;

    /* Test*/
    Solution test;
    bool res = test.isBalanced(&A);

    return 0;
}
```