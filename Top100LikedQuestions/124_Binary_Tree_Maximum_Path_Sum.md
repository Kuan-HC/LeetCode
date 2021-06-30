# 124. Binary Tree Maximum Path Sum

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any path.

[LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum)  

### Example 1:

<img src="img/124_q1.jpg" width = "300"/>

```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

```

### Example 2:

<img src="img/124_q2.jpg" width = "500"/>

```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

# 12.4 二叉樹中的最大路徑和

路徑 被定義為一條從樹中任意節點出发，沿父節點-子節點連接，達到任意節點的序列。同一個節點在一條路徑序列中 至多出現一次 。該路徑 至少包含一個 節點，且不一定經過根節點。

路徑和 是路徑中各節點值的總和。

給你一個二叉樹的根節點 root ，返回其 最大路徑和 。


## Solution

### C++
* recurrsion


```
#include <algorithm>

using namespace std;

/* Definition for a binary tree node.*/
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
    int recursion(TreeNode *root, int &maxSum)
    {
        /* end condition*/
        if (root == nullptr)
            return 0;

        /* left branch*/
        int left = max(recursion(root->left, maxSum), 0);

        /* right branch*/
        int right = max(recursion(root->right, maxSum), 0);

        /* current node*/
        int curr = root->val;

        maxSum = maxSum > left + right + curr ? maxSum : left + right + curr;

        return curr + max(left,right);
    }

public:
    int maxPathSum(TreeNode *root)
    {
        int maxSum = root->val;
        (void)recursion(root, maxSum);

        return maxSum;
    }
};

int main()
{
    /* Input*/
    TreeNode D(15), E(7), C(9);
    TreeNode B(20, &D, &E);
    TreeNode A(-10, &B, &C);
    

    /* unit test*/
    Solution test;
    int res = test.maxPathSum(&A);

    return 0;
}
```