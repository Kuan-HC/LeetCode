# 劍指 Offer 32-2 從上到下打印二叉樹 II

從上到下按層打印二叉樹，同一層的節點按從左到右的順序打印，每一層打印到一行。

### Example 1

給定二叉樹: [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其層次遍歷結果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

* 總節點數 <= 1000

[LeetCode](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

## Solution  

### C++

* 時間複雜度：O(n) N 為二叉樹的節點數量，即 BFS 需循環 N 次。

* 空間複雜度：最差情況下，即當樹為平衡二叉樹時，最多有 N/2 個樹節點同時在 queue 中，使用 O(N) 大小的額外空間。

```
#include <vector>
#include <queue>

using namespace std;

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
public:
    vector<vector<int>> levelOrder(TreeNode *root)
    {
        vector<vector<int>> ret;

        if (root == nullptr)
            return ret;

        /* initial condition*/
        queue<TreeNode *> front;
        vector<int> levelList;
        front.emplace(root);

        while (front.empty() != true)
        {
            levelList.clear();
            int lvLen = front.size();
            for (int i = 0; i < lvLen; ++i)
            {
                TreeNode *tmp = front.front();
                front.pop();

                levelList.push_back(tmp->val);

                if(tmp->left != nullptr)
                    front.emplace(tmp->left);
                if(tmp->right != nullptr)
                    front.emplace(tmp->right);
            }
            ret.emplace_back(levelList);
        }

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(3), B(9), C(20), D(15), E(7);
    A.left = &B;
    A.right = &C;
    C.left = &D;
    C.right = &E;

    /* Test*/
    Solution test;
    vector<vector<int>> res = test.levelOrder(&A);

    return 0;
}
```