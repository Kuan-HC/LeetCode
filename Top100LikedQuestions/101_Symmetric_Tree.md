# 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).  

### Example 1:
For example, this binary tree [1,2,2,3,4,4,3] is symmetric: 
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
### Example 2:
But the following [1,2,2,null,3,null,3] is not:  
```
    1
   / \
  2   2
   \   \
    3   3
```
[LeetCode](https://leetcode.com/problems/symmetric-tree/)  


# 對稱二叉樹  
給定一個二叉樹，檢查它是鏡像對稱的  

## Solution

### C++
```
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
    vector<int> inorderList;

    void inOrder(TreeNode *root)
    {
        if (root == nullptr)
            return;

        /* left branch first*/
        inOrder(root->left);
        inorderList.push_back(root->val);
        inOrder(root->right);
    }

public:
    bool isSymmetric(TreeNode *root)
    {

        inOrder(root);
        int len = inorderList.size();
        if (len & 1 == 0)
            return false;

        int left = 0;
        int right = len - 1;

        while (left <= right)
        {
            if (inorderList[left] != inorderList[right])
                return false;
            left++;
            right--;
        }

        return true;
    }
};

int main()
{
    /* Input*/
    TreeNode A(1), B(2), C(3), D(4), E(5), F(6), G(7);
    A.left = &B;
    A.right = &C;
    B.left = &D;
    B.right = &G;
    C.left = &E;
    C.right = &F;

    /* unit test*/
    Solution test;
    bool res = test.isSymmetric(&A);

    int test1 = 7 % 2;
    int test2 = 7 & (2 - 1);

    return 0;
}
```


* Note:  

1. 使用遞歸recursion 時需特別注意邊界的情況，本題的邊界狀況即為  TreeNode = Null  

2. Misra C 中禁止使用recursion 及鍊表，猜想是因為新的資料一直在生成，使用recursion沒有辦法終止  
   如果是固定的資料，也不應該每次啟動時重新計算 
