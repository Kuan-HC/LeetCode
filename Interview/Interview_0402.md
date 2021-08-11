# 面試金典 0402  最小高度樹

給定一個有序整數數組，元素各不相同且按升序排列，編寫一個算法，創建一棵高度最小的二叉搜索樹。

### example

```
給定有序數組: [-10,-3,0,5,9],

一個可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面這個高度平衡二叉搜索樹：

          0 
         / \ 
       -3   9 
       /   / 
     -10  5 
```

[LeetCode](https://leetcode-cn.com/problems/minimum-height-tree-lcci/)



## Solution  

### C++

* 時間複雜度 O(n) 需遍曆所有的點

* 空間複雜度 O(log n) 每一次建立node均將列拆為1/2

```
#include <vector>

using namespace std;

/*   Definition for a binary tree node. */
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
    TreeNode *buildNode(vector<int> &nums, int start, int end)
    {
        if(start ==end)
            return new TreeNode(nums[start]);
        else if( start > end)
            return nullptr;

        int mid = start + (end - start) / 2;

        TreeNode *root = new TreeNode(nums[mid]);

        /* left branch*/
        root->left = buildNode(nums, start, mid - 1);
        /*right branch*/
        root->right = buildNode(nums, mid + 1, end);

        return root;
    }

public:
    TreeNode *sortedArrayToBST(vector<int> &nums)
    {
        int left = 0;
        int right = nums.size() - 1;

        TreeNode *ret = buildNode(nums, left, right);
        return ret;
    }
};

int main()
{
    /* input*/
    vector<int> input = {-10, -3, 0, 5, 9};

    /* Test*/
    Solution test;
    test.sortedArrayToBST(input);

    return 0;
}
```