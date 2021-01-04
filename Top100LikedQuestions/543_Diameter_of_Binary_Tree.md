#  543. Diameter of Binary Tree
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

[LeetCode](https://leetcode.com/problems/hamming-distance/)

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


#  漢明距離
兩個整數之間的漢明距離指的是這兩個數字對應二進制位不同的位置的數目。

給出兩個整數 x 和 y，計算它們之間的漢明距離。


# Solution  

## C

```
int hammingDistance(int x, int y)
{
    x = x ^ y;
    y = 0;

    while (x)
    {
        if (x & 0x1)
            ++y;
        x >>= 1;
    }

    return y;
}
```


