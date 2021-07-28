# 劍指 Offer 54 二叉搜索樹的第k大節點
給定一棵二叉搜索樹，請找出其中第k大的節點。

[LeetCode](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

### Example 1
```
輸入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
輸出: 4
```
### Example 2
```
輸入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
輸出: 4
```

* 1 ≤ k ≤ 二叉搜索樹元素個數

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
    int ret{0};
    int count{0};
    bool found{false};

    void DFS(TreeNode *root, int &k)
    {

        if (root == nullptr)
            return;

        /* right branch first*/
        DFS(root->right, k);
        /* Inorder Traversal*/
        if(found ==true)
            return;

        count++;
        if (count == k)
        {
            found = true;
            ret = root->val;
            return;
        }
        DFS(root->left, k);
    }

public:
    int kthLargest(TreeNode *root, int k)
    {
        DFS(root, k);

        return ret;
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
    int res = test.kthLargest(&A, 2);

    return 0;
}
```