# 面試金典 0409 二叉搜索樹序列

從左向右遍歷一個數組，通過不斷將其中的元素插入樹中可以逐步地生成一棵二叉搜索樹。給定一個由不同節點組成的二叉搜索樹，輸出所有可能生成此樹的數組。

## BST Sequences

A binary search tree was created by traversing through an array from left to right and inserting each element. 
Given a binary search tree with distinct elements, print all possible arrays that could have led to this tree.
 
[LeetCode](https://leetcode-cn.com/problems/bst-sequences-lcci/)

### Example 1
```
        2
       / \
      1   3
```

Output:
```
[
   [2,1,3],
   [2,3,1]
]
```


### C++ 


```
#include <vector>
#include <queue>

using namespace std;

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
    vector<vector<int>> ret;
    void dfs(queue<TreeNode *> frontier, vector<int> &list)
    {
        if (frontier.empty() == true) // 當queue裡沒東西時，存到ret裡
        {
            ret.emplace_back(list);
            return;
        }

        int len = frontier.size();
        
        for (int i = 0; i < len; i++)
        {
            //取得當前node
            TreeNode *temp = frontier.front();
            frontier.pop();
            //當前值加入path
            list.push_back(temp->val);

            //將該點的分支加入給下一層的queue
            queue<TreeNode *> next = frontier;
            if (temp->left != nullptr)
                next.push(temp->left);
            if (temp->right != nullptr)
                next.push(temp->right);
            
            // 探索下一個
            dfs(next, list);

            list.erase(list.end() - 1);
            frontier.push(temp);
            printf("debug");
        }
    }

public:
    vector<vector<int>> BSTSequences(TreeNode *root)
    {
        if (root == nullptr)
            return {{}};

        queue<TreeNode *> frontier;
        frontier.push(root);
        vector<int> list;

        dfs(frontier, list);

        return ret;
    }
};

int main(void)
{
    /* input*/
    TreeNode D(0), E(4), B(1), C(3), A(2);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    //C.right = &E;

    Solution test;
    vector<vector<int>> res = test.BSTSequences(&A);

    return 0;
}
```
