# 面試金典 0410 檢查子樹

檢查子樹。你有兩棵非常大的二叉樹：T1，有幾萬個節點；T2，有幾萬個節點。設計一個算法，判斷 T2 是否為 T1 的子樹。

如果 T1 有這麽一個節點 n，其子樹與 T2 一模一樣，則 T2 為 T1 的子樹，也就是說，從節點 n 處把樹砍斷，得到的樹與 T2 完全相同。

來源：力扣（LeetCode）
鏈接：https://leetcode-cn.com/problems/check-subtree-lcci


 
##  Check Subtree
T1 and T2 are two very large binary trees. Create an algorithm to determine if T2 is a subtree of T1.

A tree T2 is a subtree of T1 if there exists a node n in T1 such that the subtree of n is identical to T2. That is, if you cut off the tree at node n, the two trees would be identical.

[LeetCode](https://leetcode-cn.com/problems/check-subtree-lcci)


### Example 1

```
Input: t1 = [1, 2, 3], t2 = [2]
Output: true
```

### Example 2

```
Input: t1 = [1, null, 2, 4], t2 = [3, 2]
Output: false
```

### C++ 


```
/* * Definition for a binary tree node. */
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
    bool isNodeEqual(TreeNode *t1, TreeNode *t2)
    {
        if (t1 == nullptr && t2 == nullptr)
            return true;
        else if (t1 == nullptr || t2 == nullptr || t1->val != t2->val)
            return false;
        
        return isNodeEqual(t1->left, t2->left) && isNodeEqual(t1->right, t2->right);        
    }

public:
    bool checkSubTree(TreeNode *t1, TreeNode *t2)
    {
        if (t1 == nullptr && t2 == nullptr)
            return true;
        else if (t1 == nullptr || t2 == nullptr)
            return false;

        return isNodeEqual(t1,t2) || checkSubTree(t1->left, t2) || checkSubTree(t1->right, t2);
    }
};

int main()
{
    /* input */
    TreeNode A(1), B(2), C(3), D(2);
    A.left = &B;
    A.right = &C;

    /* test*/
    Solution test;
    bool res = test.checkSubTree(&A, &D);

    return 0;
}
```
