# 461. Hamming Distance
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

[LeetCode](https://leetcode.com/problems/hamming-distance/)

### Example :
```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```

#  漢明距離
兩個整數之間的漢明距離指的是這兩個數字對應二進制位不同的位置的數目。

給出兩個整數 x 和 y，計算它們之間的漢明距離。


## Solution  

### C

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


