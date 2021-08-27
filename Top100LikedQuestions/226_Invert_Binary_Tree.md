# 226. Invert Binary Tree
Invert a binary tree.

[LeetCode](https://leetcode.com/problems/invert-binary-tree/)

### Example :
Input:
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
Output:
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
#  翻轉二叉樹
反轉一個單鍊表


## Solution  
### recursion

### C++

```
class Solution
{
private:
    void dfs(TreeNode *root)
    {
        if(root == nullptr)
            return;

        TreeNode *tmp = root->left;
        root->left = root->right;
        root->right = tmp;

        /*left branch*/
        dfs(root->left);
        dfs(root->right);

    }
public:
    TreeNode *invertTree(TreeNode *root)
    {
        dfs(root);

        return root;
    }
};
```


### C

```
struct TreeNode* invertTree(struct TreeNode* root){
    if (root == NULL)
        return 0;
    
    if((root->left == NULL) && (root->right == NULL))
        return root;
    
    struct TreeNode* tmp = root->left; 
    root->left = root->right;
    root->right = tmp;

    invertTree(root->left);
    invertTree(root->right);

    return root;
}
```


