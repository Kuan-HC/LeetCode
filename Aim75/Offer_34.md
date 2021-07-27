# 劍指 Offer 34 二叉樹中和為某一值的路徑

輸入一棵二叉樹和一個整數，打印出二叉樹中節點值的和為輸入整數的所有路徑。從樹的根節點開始往下一直到葉節點所經過的節點形成一條路徑。

[LeetCode](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)
 

### Example 1

```
給定如下二叉樹，以及目標和 target = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

* 節點總數 <= 10000

## Solution  

### C++

* 時間複雜度：O(N) ： N 為二叉樹的節點數，先序遍歷需要遍歷所有節點

* 空間複雜度：O(N) ： 最差情況下，即樹退化為鏈表時，path 存儲所有樹節點，使用 O(N) 額外空間。

```
#include <vector>

using namespace std;

/**  Definition for a binary tree node.*/
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution
{
private:
    vector<vector<int>> ret;
    vector<int> path;

    void DFS(TreeNode *root, int &target, int &lvSum)
    {
        if(root == nullptr)
            return;

        lvSum += root->val;
        path.push_back(root->val);
        if(lvSum == target && root->left == nullptr && root->right == nullptr)
            ret.emplace_back(path);

        DFS(root->left, target, lvSum);
        DFS(root->right, target, lvSum);

        lvSum -= root->val;;
        path.pop_back();       
    }

public:
    vector<vector<int>> pathSum(TreeNode *root, int target)
    {
        int sum = 0;
        DFS(root, target, sum);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(1), B(2), C(8), D(11), E(13), F(4);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    C.left = &E;
    C.right = &F;

    /* Test*/
    Solution test;
    vector<vector<int>> res = test.pathSum(&A, 1);

    return 0;
}
```