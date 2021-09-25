# 面試金典 0412 求合路徑

給定一棵二叉樹，其中每個節點都含有一個整數數值(該值或正或負)。設計一個算法，打印節點數值總和等於某個給定值的所有路徑的數量。
注意，路徑不一定非得從二叉樹的根節點或葉節點開始或結束，但是其方向必須向下(只能從父節點指向子節點方向)。

## Paths with Sum

You are given a binary tree in which each node contains an integer value (which might be positive or negative). 
Design an algorithm to count the number of paths that sum to a given value. 
The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).
 
[LeetCode](https://leetcode-cn.com/problems/paths-with-sum-lcci/)

### Example 1
```
Given the following tree and  sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

Output:
```
3
Explanation: Paths that have sum 22 are: [5,4,11,2], [5,8,4,5], [4,11,7]
```
* node number <= 10000

### C++ 

* 空間複雜度 O(n)

* 時間複雜度 O(n)

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
    unordered_map<int, int> prefix;
    int target{0};
    int dfs(TreeNode *root, int &nodeSum)
    {
        if (root == nullptr)
            return 0;

        nodeSum += root->val;
        //多少個存在prefix的數值符合要求
        int match = prefix[nodeSum - target];

        prefix[nodeSum]++;       
        int left = dfs(root->left, nodeSum);
        int right = dfs(root->right, nodeSum);
        prefix[nodeSum]--;
        nodeSum -= root->val;

        return match + left + right;
    }

public:
    int pathSum(TreeNode *root, int sum)
    {
        target = sum;
        int tempSum = 0;
        prefix[0] = 1;

        return dfs(root, tempSum);
    }
};

int main(void)
{
    /* input*/
    TreeNode B(4), C(8), A(1);
    A.left = &B;
    A.right = &C;

    Solution test;
    int res = test.pathSum(&A, 5);

    return 0;
}
```
