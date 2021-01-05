# 543. Diameter of Binary Tree
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

[LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/)

### Example :
```
          1
         / \
        2   3
       / \     
      4   5    
```

### Note
The length of path between two nodes is represented by the number of edges between them.


#  二叉樹的直徑
給定一棵二叉樹，你需要計算它的直徑長度。一棵二叉樹的直徑長度是任意兩個結點路徑長度中的最大值。這條路徑可能穿過也可能不穿過根結點。

# Solution  

## C

```
#define MAX(x, y) (x > y ? x : y)

int depth(struct TreeNode *root, int *length)
{
    if (root == NULL)
        return 0;

    int left = depth(root->left, length);
    int right = depth(root->right, length);
    
    if((left + right) > *length)
        *length = left + right;
    
    return (MAX(left, right) + 1);
}

int diameterOfBinaryTree(struct TreeNode *root)
{
    if (root == NULL)
        return 0;

    int max_length = 0;
    (void)depth(root, &max_length);

    return max_length;
}
```


