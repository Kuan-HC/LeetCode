# 劍指 Offer 62 圓圈中最後剩下的數字

0,1,···,n-1這n個數字排成一個圓圈，從數字0開始，每次從這個圓圈里刪除第m個數字（刪除後從下一個數字開始計數）。求出這個圓圈里剩下的最後一個數字。

例如，0、1、2、3、4這5個數字組成一個圓圈，從數字0開始每次刪除第3個數字，則刪除的前4個數字依次是2、0、4、1，因此最後剩下的數字是3。

[LeetCode](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

### Example 1

```
輸入: n = 5, m = 3
輸出: 3
```

### Example 2

```
輸入: n = 10, m = 17
輸出: 2

```

* 1 <= n <= 10^5
* 1 <= m <= 10^6


## Solution  

<img src="img/62.jpg" width = "600"/>

從最後剩下的 3 倒著看，我們可以反向推出這個數字在之前每個輪次的位置。

最後剩下的 3 的下標是 0。

第四輪反推，補上 mmm 個位置，然後模上當時的數組大小 222，位置是(0 + 3) % 2 = 1。

第三輪反推，補上 mmm 個位置，然後模上當時的數組大小 333，位置是(1 + 3) % 3 = 1。

第二輪反推，補上 mmm 個位置，然後模上當時的數組大小 444，位置是(1 + 3) % 4 = 0。

第一輪反推，補上 mmm 個位置，然後模上當時的數組大小 555，位置是(0 + 3) % 5 = 3。

所以最終剩下的數字的下標就是3。因為數組是從0開始的，所以最終的答案就是3。

總結一下反推的過程，就是 (當前index + m) % 上一輪剩余數字的個數。

### C++

* 時間複雜度：O(n) : n 數字

* 空間複雜度：O(1) 

```
class Solution
{
public:
    int lastRemaining(int n, int m)
    {
        /* we could use a for loop to calculate the position in length = N
           list, base on the position already know from length = N-1*/

        /* we want to know in length = 1, the last one
         * also the first one*/
        int position = 0;
        for (int len = 2; len <= n; ++len)
        {
            position = (position + m )%len;
        }

        return position;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    bool res = test.lastRemaining(5,3);

    return 0;
}
```