# 劍指 Offer 32-3 從上到下打印二叉樹 III

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
  [20,9],
  [15,7]
]
```

* 總節點數 <= 1000

[LeetCode](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

## Solution  

### C++

* 時間複雜度：O(n) N 為二叉樹的節點數量，即 BFS 需循環 N 次。

* 空間複雜度：最差情況下，即當樹為平衡二叉樹時，最多有 N/2 個樹節點同時在 queue 中，使用 O(N) 大小的額外空間。

```
#include <vector>
#include <queue>
#include <algorithm>

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

        queue<TreeNode *> front;
        vector<int> tmpVec;
        front.push(root);
        bool oddLv = true;
        /* set initial condition*/
        while (front.empty() != true)
        {
            tmpVec.clear();
            int lvLen = front.size();
            oddLv = oddLv ? false : true;
            for (int i = 0; i < lvLen; ++i)
            {
                TreeNode *tmp = front.front();
                front.pop();

                tmpVec.push_back(tmp->val);

                if (tmp->left != nullptr)
                    front.push(tmp->left);

                if (tmp->right != nullptr)
                    front.push(tmp->right);
            }
            if(oddLv == true)
                reverse(tmpVec.begin(), tmpVec.end());
            ret.emplace_back(tmpVec);
        }
        return ret;
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
    vector<vector<int>> res = test.levelOrder(&A);

    return 0;
}
```