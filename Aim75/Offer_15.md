# 劍指 Offer 15 二進制中1的個數

編寫一個函數，輸入是一個無符號整數（以二進制串的形式），返回其二進制表達式中數字位數為 '1' 的個數（也被稱為 漢明重量).）。

[LeetCode](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)


### Example 1

```
輸入：n = 11 (控制台输入 00000000000000000000000000001011)
輸出：3
解釋：輸入的二進制串 00000000000000000000000000001011 中，共有三位為 '1'。

```

## Solution  


### C++

* 時間覆雜度: O(n) 

* 空間覆雜度: O(1) 


```
class Solution
{
public:
    int hammingWeight(uint32_t n)
    {
        int ret = 0;
        while (n != 0)
        {
            if (n & 0b1)
                ret++;

            n = n >> 1;
        }

        return ret;
    }
};

int main()
{
    /* input*/
    uint32_t input = 11;

    /* Test*/
    Solution test;
    int res = test.hammingWeight(input);

    return 0;
}
```