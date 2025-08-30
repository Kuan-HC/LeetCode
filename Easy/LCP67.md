# LCP67 裝飾樹

力扣嘉年華上的 DIY 手工展位準備了一棵縮小版的 二叉 裝飾樹 root 和燈飾，你需要將燈飾逐一插入裝飾樹中，要求如下：

完成裝飾的二叉樹根結點與 root 的根結點值相同
若一個節點擁有父節點，則在該節點和他的父節點之間插入一個燈飾（即插入一個值為 -1 的節點）。具體地：
在一個 父節點 x 與其左子節點 y 之間添加 -1 節點， 節點 -1、節點 y 為各自父節點的左子節點，
在一個 父節點 x 與其右子節點 y 之間添加 -1 節點， 節點 -1、節點 y 為各自父節點的右子節點，
現給定二叉樹的根節點 root ，請返回完成裝飾後的樹的根節點。 示例 1：
 
[LeetCode](https://leetcode.cn/problems/KnLfVT/)

### Example 1

<img src="img/lcp67_1.png" width = "250"/>

```
輸入： root = [7,5,6]

輸出：[7,-1,-1,5,null,null,6]

解釋：如下圖所示，
```

### Example 2

<img src="img/lcp67_2.png" width = "250"/>

```
輸入： root = [3,1,7,3,8,null,4]

輸出：[3,-1,-1,1,null,null,7,-1,-1,null,-1,3,null,null,8,null,4]

解釋：如下圖所示
```

### Constraints

* 0 <= root.Val <= 1000 root 節點數量範圍為 [1, 10^5]

### C++ 

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* expandBinaryTree(TreeNode* root) {
        /*
            使用前序遍歷，若一個節點有左子節點，先插入一個-1在左邊，再繼續
        */
        if(root->left){
            TreeNode* leftChild = root->left;
            root->left = new TreeNode(-1);
            root->left->left = leftChild;
            (void)expandBinaryTree(leftChild);
        }

        if(root->right){
            TreeNode* rightChild = root->right;
            root->right = new TreeNode(-1);
            root->right->right = rightChild;
            (void)expandBinaryTree(rightChild);
        }
        

        return root;
    }
};
```