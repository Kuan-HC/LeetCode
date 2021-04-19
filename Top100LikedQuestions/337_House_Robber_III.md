# 337. House Robber III
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root.

Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.

[LeetCode](https://leetcode.com/problems/house-robber-iii)

### Example 1:
<img src="img/337_q1.jpg" width = "500"/>

```
Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

### Example 2:
<img src="img/337_q2.jpg" width = "500"/>

```
Input: root = [3,4,5,1,3,null,1]
Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

#  打家劫舍
在上次打劫完一條街道之後和一圈房屋後，小偷又发現了一個新的可行竊的地區。這個地區只有一個入口，我們稱之為“根”。 除了“根”之外，每棟房子有且只有一個“父“房子與之相連。一番偵察之後，聰明的小偷意識到“這個地方的所有房屋的排列類似於一棵二叉樹”。 如果兩個直接相連的房子在同一天晚上被打劫，房屋將自動報警。

計算在不觸動警報的情況下，小偷一晚能夠盜取的最高金額。


## Solution  
### Dynamic Programming

### C

```
struct TreeNode
{
  int val;
  struct TreeNode *left;
  struct TreeNode *right;
};

int max(int a, int b){
   return a > b ? a : b;
}

struct nodeState
{
  int included;
  int notInclude;
};

struct nodeState DFS(struct TreeNode *root)
{
  struct nodeState tmp;
  if (root == NULL)
  {
    tmp.included = 0;
    tmp.notInclude  = 0;
    return tmp;
  }

  struct nodeState left = DFS(root->left);
  struct nodeState right = DFS(root->right);

  tmp.included = root->val + left.notInclude + right.notInclude;
  tmp.notInclude = max(left.included, left.notInclude) + max(right.included, right.notInclude);

  return tmp;
}

int rob(struct TreeNode *root)
{
  struct nodeState ret = DFS(root);

  return max(ret.included, ret.notInclude);
}

int main()
{
  /* input*/
  struct TreeNode A, B, C, D, E, F;
  A.val = 3;
  A.left = &B;
  A.right = &C;
  B.val = 4;
  B.left = &D;
  B.right = &E;
  C.val = 5;
  C.left = NULL;
  C.right = &F;
  D.val = 2;
  D.left = NULL;
  D.right = NULL;
  E.val = 2;
  E.left = NULL;
  E.right = NULL;
  F.val = 1;
  F.left = NULL;
  F.right = NULL;

  /* Algorithm*/
  int res = rob(&A);

  return 0;
}
```


