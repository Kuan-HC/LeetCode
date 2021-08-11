# 面試金典 0403  特定深度節點鏈表

給定一棵二叉樹，設計一個算法，創建含有某一深度上所有節點的鏈表（比如，若一棵樹的深度為 D，則會創建出 D 個鏈表）。返回一個包含所有深度的鏈表的數組。

[LeetCode](https://leetcode-cn.com/problems/list-of-depth-lcci/)

### example

```
輸入：[1,2,3,4,5,null,7,8]

        1
       /  \ 
      2    3
     / \    \ 
    4   5    7
   /
  8

輸出：[[1],[2,3],[4,5,7],[8]]
```

## Solution  

### C++

* 時間複雜度 O(n) 需遍曆所有的點

* 空間複雜度 O(1) 1

```
#include <vector>
#include <queue>

using namespace std;

/* Definition for a binary tree node. */
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

/*  Definition for singly-linked list. */
struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};


class Solution
{
private:
    vector<ListNode *> ret;

    void bfs(TreeNode *root)
    {
        queue<TreeNode *> front;

        /* set bfs starting point*/
        front.push(root);
        int levelLength = 0;

        ListNode levelHead(0);
        ListNode *tail = &levelHead;

        while (front.empty() != true)
        {
            levelLength = front.size();

            tail = &levelHead;
            for (int i = 0; i < levelLength; ++i)
            {
                TreeNode *tmp = front.front();
                front.pop();
                tail->next = new ListNode(tmp->val);
                tail = tail->next;

                if(tmp->left != nullptr)
                    front.push(tmp->left);
                if(tmp->right != nullptr)
                    front.push(tmp->right);
            }
            ret.push_back(levelHead.next);
        }
    }

public:
    vector<ListNode *> listOfDepth(TreeNode *tree)
    {
        if (tree == nullptr)
            return ret;

        bfs(tree);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(0), B(1), C(2), D(3), E(4);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    C.left = &E;

    /* Test*/
    Solution test;
    vector<ListNode *> ret = test.listOfDepth(&A);

    return 0;
}
```