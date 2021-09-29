# 面試金典 1712 BiNode

二叉樹數據結構TreeNode可用來表示單向鏈表（其中left置空，right為下一個鏈表節點）。實現一個方法，把二叉搜索樹轉換為單向鏈表，要求依然符合二叉搜索樹的性質，轉換操作應是原址的，也就是在原始的二叉搜索樹上直接修改。

返回轉換後的單向鏈表的頭節點。

## BiNode

The data structure TreeNode is used for binary tree, but it can also used to represent a single linked list (where left is null, and right is the next node in the list). Implement a method to convert a binary search tree (implemented with TreeNode) into a single linked list. The values should be kept in order and the operation should be performed in place (that is, on the original data structure).

Return the head node of the linked list after converting.
 
[LeetCode](https://leetcode-cn.com/problems/binode-lcci/)

### Example 1
```
Input:  [4,2,5,1,3,null,6,0]
Output:  [0,null,1,null,2,null,3,null,4,null,5,null,6]

```

### C++ 

* 時間複雜度 O(N)

* 空間複雜度 O(N)

```
class Solution
{
private:
    TreeNode head{-1};
    TreeNode *tail{nullptr};

    void inorder(TreeNode *root)
    {
        if (root == nullptr)
            return;

        /* left branch*/
        inorder(root->left);

        /* process this node*/
        if (tail == nullptr)
        {
            tail = root;
            head.right = tail;
        }
        else
        {
            tail->right = root;
            tail = tail->right;  
        }        
        tail ->left = nullptr;

        /* right branch*/
        inorder(root->right);
    }

public:
    TreeNode *convertBiNode(TreeNode *root)
    {
        if (root == nullptr)
            return root;

        inorder(root);

        return head.right;
    }
};
```
