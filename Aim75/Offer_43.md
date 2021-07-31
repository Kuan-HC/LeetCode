# 劍指 Offer 43 1～n 整數中 1 出現的次數

輸入一個整數 n ，求1～n這n個整數的十進制表示中1出現的次數。

[LeetCode](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

### Example 1
```
輸入：n = 12
輸出：5
輸入12，1～12這些整數中包含1 的數字有1、10、11和12，1一共出現了5次。
```

### Example 1
```
輸入：n = 13
輸出：6
```

* 1 <= n < 2^31


## Solution  

### C++

* 時間複雜度：O(n) : while 循環內的計算操作使用 O(1) 時間；循環次數為數字 n 的位數，即 log 10  n ，因此循環使用 O(log n) 時間。

* 空間複雜度：O(1) : O(N)=O(5)=O(1) ： 幾個變量使用常數大小的額外空間。
```
class Solution
{
public:
    int countDigitOne(int n)
    {
        int left = n;
        int right = 0;
        int curr = 0;
        int factor = 1;
        int count = 0;

        while (left != 0 )
        {
            curr = left % 10;
            left /= 10;

            if (curr > 1)
                count += left * factor + factor;
            else if (curr == 1)
                count += left * factor + right + 1;
            else
                count += left * factor;

            right = factor * curr + right;
            if (left > 0)
                factor *= 10;
        }
        return count;
    }
};

int main()
{

    /* Test*/
    Solution test;
    int res = test.countDigitOne(13);

    return 0;
}

```