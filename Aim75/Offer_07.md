# 劍指 Offer 07 重建二叉樹

輸入某二叉樹的前序遍歷和中序遍歷的結果，請重建該二叉樹。假設輸入的前序遍歷和中序遍歷的結果中都不含重覆的數字。
 
[LeetCode](https://leetcode-cn.com/problems/problems/zhong-jian-er-cha-shu-lcof/)


### Example 1
```
前序遍歷 preorder = [3,9,20,15,7]
中序遍歷 inorder = [9,3,15,20,7]
```

* 0 <= 節點個數 <= 5000

## Solution  


### C++

* 時間複雜度: O(n) 

* 空間複雜度: O(n) 

```
#include <vector>
#include <unordered_map>

using namespace std;

/*
  Definition for a binary tree node.*/
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
    unordered_map<int, int> inMap;
    

    TreeNode *recursion(int preStart, int preLen, int inStart, int inLen, vector<int> &preorder, vector<int> &inorder)
    {
        if (preLen == 0)
            return nullptr;

        int midValue = preorder[preStart];
        int midIdInList = inMap[midValue];
        int leftLen = midIdInList - inStart;
        int rightLen = preLen - leftLen - 1;

        TreeNode *midNode = new TreeNode(midValue);

        midNode->left = recursion(preStart + 1, leftLen, midIdInList - leftLen, leftLen, preorder, inorder);

        midNode->right = recursion(preStart + leftLen + 1, rightLen, midIdInList + 1, rightLen, preorder, inorder);

        return midNode;
    }

public:
    TreeNode *buildTree(vector<int> &preorder, vector<int> &inorder)
    {
        int len = preorder.size();

        if (len == 0)
            return nullptr;

        for (int i = 0; i < len; ++i)
            inMap[inorder[i]] = i;
            
        

        TreeNode *ret = recursion(0, len, 0, len, preorder, inorder);

        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    /* Test*/
    Solution test;
    TreeNode *res = test.buildTree(preorder, inorder);

    return 0;
}
```