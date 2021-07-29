# 劍指 Offer 65 不用加减乘除做加法

寫一個函數，求兩個整數之和，要求在函數體內不得使用 “+”、“-”、“*”、“/” 四則運算符號。

[LeetCode](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcoff/)

### Example 1
```
輸入: a = 1, b = 1
輸出: 2
 ```

* a, b 均可能是負數或 0
* 結果不會溢出 32 位整數


## Solution  



### C++

* 時間複雜度：O(1) : 最差情況下（例如 a =a= 0x7fffffff , b = 1b=1 時），需循環 32 次，使用 O(1) 時間；每輪中的常數次位操作使用 O(1) 時間

* 空間複雜度：O(1) 使用常數大小的額外空間

* 對負數的位移，在C++在沒有定義其行為，故加上(unsigned)

```
class Solution
{
public:
    int add(int a, int b)
    {
        int computeXor = a ^ b;
        int computeAnd = (unsigned)(a & b) << 1;
        int tmp = 0;

        while (computeAnd != 0)
        {
            tmp =  computeXor ^ computeAnd;
            computeAnd = (unsigned)(computeXor & computeAnd) << 1;
            computeXor = tmp;
        }

        return computeXor;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    bool res = test.add(-1, 2);

    return 0;
}
```