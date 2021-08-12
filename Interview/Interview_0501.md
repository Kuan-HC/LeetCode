# 面試金典 0501 插入

給定兩個整型數字 N 與 M，以及表示比特位置的 i 與 j（i <= j，且從 0 位開始計算）。

編寫一種方法，使 M 對應的二進制數字插入 N 對應的二進制數字的第 i ~ j 位區域，不足之處用 0 補齊。具體插入過程如圖所示。

題目保證從 i 位到 j 位足以容納 M， 例如： M = 10011，則 i～j 區域至少可容納 5 位。

[LeetCode](https://leetcode-cn.com/problems/insert-into-bits-lcci/)
 

### Example 1
```
輸入：N = 1024(10000000000), M = 19(10011), i = 2, j = 6
輸出：N = 1100(10001001100)
```

### Example 2
```
輸入： N = 0, M = 31(11111), i = 0, j = 4
輸出：N = 31(11111)
```


```

## Solution  

### C++

* 時間複雜度 O(n) n為i-j的長度

* 空間複雜度 O(1) 

```
class Solution
{
public:
    int insertBits(int N, int M, int i, int j)
    {
        /* remove bit i - j & */
        for (int k = i; k <= j; ++k)
        {
            if (N & (1 << k))
                N -= (1 << k);
        }

        N += (M << i);

        return N;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int ret = test.insertBits(0, 31, 0, 4);

    return 0;
}
```