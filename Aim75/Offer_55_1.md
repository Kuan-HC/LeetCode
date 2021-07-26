# 劍指 Offer 55-1 二叉樹的深度

輸入一棵二叉樹的根節點，求該樹的深度。從根節點到葉節點依次經過的節點（含根、葉節點）形成樹的一條路徑，最長路徑的長度為樹的深度。


[LeetCode](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

### Example 1

```

    3
   / \
  9  20
    /  \
   15   7

返回它的最大深度 3 
```

* 節點總數 <= 10000

## Solution  

### C++

* 時間複雜度：O(n) n 為樹的節點數量，計算樹的深度需要遍歷所有節點

* 空間複雜度：O(n) 最差情況下（當樹退化為鏈表時），遞歸深度可達到 n 。


```
/*  Definition for a binary tree node.*/
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
    int depth{0};
    void DFS(TreeNode *root, int currDepth)
    {
        if (root == nullptr)
            return;

        depth = depth > currDepth ? depth : currDepth;

        DFS(root->left, currDepth+1);
        DFS(root->right, currDepth+1);
    }

public:
    int maxDepth(TreeNode *root)
    {
        DFS(root, 1);

        return depth;
    }
};

int main()
{
    /* input*/
    TreeNode A(1), B(2), C(3), D(4), E(5);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    C.right = &E;

    /* Test*/
    Solution test;
    int res = test.maxDepth(&A);

    return 0;
}
```