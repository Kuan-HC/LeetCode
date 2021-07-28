# 劍指 Offer 44 數字序列中某一位的數字

數字以0123456789101112131415…的格式序列化到一個字符序列中。在這個序列中，第5位（從下標0開始計數）是5，第13位是1，第19位是4，等等。

請寫一個函數，求任意第n位對應的數字。

 [LeetCode](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

### Example 1

```
輸入：n = 3
輸出：3
```

### Example 2

```
輸入：n = 11
輸出：0
```

* 0 <= n < 2^31

## Solution  

### C++

* 時間複雜度：O(log N) Step 1確定位數時需要 log N

* 空間複雜度：O(1) 


```
#include <cmath>

using namespace std;

class Solution
{
public:
    int findNthDigit(int n)
    {
        if (n <= 9)
            return n;
        /* step 1: figure out how many digits*/
        int digitNum = 1;
        int numbersLen = 9;
        int totalLen = 9; // digitNum * numbersLen
        int leftLimit = 0;

        while (n > totalLen)
        {
            n -= totalLen;
            digitNum++;
            leftLimit += numbersLen;
            numbersLen *= 10;
            totalLen = digitNum * numbersLen;
        }

        /* Step 2: figure out the value*/
        int valueOffset = (n - 1) / digitNum + 1;
        int value = leftLimit + valueOffset;

        /*  Step 3: figure out the digit*/
        n = (digitNum - (n % digitNum)) % digitNum;
        int ret = (value / pow(10, n));
        ret %= 10;

        return ret;
    }
};

int main()
{
    /* input*/
    //vector<int> input = {3, 4, 3, 3};

    /* Test*/
    Solution test;
    int res = test.findNthDigit(12);

    return 0;
}
```