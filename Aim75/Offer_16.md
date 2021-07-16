# 劍指 Offer 16 數值的整數次方

實現 pow(x, n) ，即計算 x 的 n 次冪函數（即，xn）。不得使用庫函數，同時不需要考慮大數問題。

 
[LeetCode](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)


### Example 1

```
輸入：x = 2.00000, n = 10
輸出：1024.00000
```

### Example 2

```
輸入：x = 2.10000, n = 3
輸出：9.26100
```



* -100.0 < x < 100.0
* -231 <= n <= 231-1
* -104 <= xn <= 104

## Solution  


### C++

* 時間覆雜度：O(log n) 即為遞歸的層數。

* 空間覆雜度：O(log n) 即為遞歸的層數。這是由於遞歸的函數調用會使用棧空間。



```
class Solution
{
private:
    double recursionPow(double x, int deg)
    {
        if (deg == 0)
            return 1;

        double tmp = recursionPow(x, deg / 2);
        if (deg % 2 == 1)
            return tmp*tmp *x;
        else 
            return tmp*tmp;
    }

public:
    double myPow(double x, int n)
    {
        int degree = n;

        double res = n > 0 ? recursionPow(x, degree) : 1 / recursionPow(x, -degree);

        return res;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    double res = test.myPow(2, -3);

    return 0;
}
```