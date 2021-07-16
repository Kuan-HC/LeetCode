# 劍指 Offer 28 對稱的二叉樹

請實現一個函數，用來判斷一棵二叉樹是不是對稱的。如果一棵二叉樹和它的鏡像一樣，那麽它是對稱的。

[LeetCode](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

例如，二叉樹 [1,2,2,3,4,4,3] 是對稱的。
 
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
但是下面這個 [1,2,2,null,3,null,3] 則不是鏡像對稱的:

```
    1
   / \
  2   2
   \   \
   3    3
```

### Example 1

```
輸入：root = [1,2,2,3,4,4,3]
輸出：true
```


* 0 <= 節點數 <= 1000

## Solution  


### C++

* 時間複雜度: O(n) 

* 空間複雜度: O(n) 


```
using namespace std;

/* Definition for singly-linked list. */
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
    void compNode(TreeNode *left, TreeNode *right, bool &identical)
    {
        /* stop recursion condition*/
        if (left == nullptr && right == nullptr)
            return;
        else if (left == nullptr || right == nullptr)
        {
            identical = false;
            return;
        }

        if (left->val == right->val)
        {
            compNode(left->left, right->right, identical);
            if (identical == true)
                compNode(left->right, right->left, identical);
        }
        else
            identical = false;
    }

public:
    bool isSymmetric(TreeNode *root)
    {
        if (root == nullptr)
            return true;

        /* compare left and right nodes*/
        bool ret = true;
        compNode(root->left, root->right, ret);

        return ret;
    }
};

int main()
{
    /* input*/
    TreeNode A(1), B(2), C(2), D(3), E(4), F(4), G(3);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    B.right = &E;
    C.left = &F;
    C.right = &G;

    /* Test*/
    Solution test;
    bool res = test.isSymmetric(&A);

    return 0;
}
```