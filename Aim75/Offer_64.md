# 劍指 Offer 66 求1+2+…+n

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等關鍵字及條件判斷語句
（A?B:C）。

[LeetCode](https://leetcode-cn.com/problems/qiu-12n-lcof/)

### Example 1
```
輸入: n = 3
輸出: 6
```

### Example 2
```
輸入: n = 9
輸出: 45
```

## Solution  

### C++

* 時間複雜度：O(n) : recursion的深度 n

* 空間複雜度：O(n) recursion的深度 n

```
class Solution
{
public:
    int sumNums(int n)
    {
        n && (n += sumNums(n-1));

        return n ;
    }
};
```

```
class Solution
{
public:
    int sumNums(int n)
    {
        if (n == 0)
            return 0;

        return n + sumNums(n - 1);
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int res = test.sumNums(2);

    return 0;
}
```