# 面試金典 0506 整數轉換

整數轉換。編寫一個函數，確定需要改變幾個位才能將整數A轉成整數B。

[LeetCode](https://leetcode-cn.com/problems/convert-integer-lcci/)

### Example 1
```
輸入：A = 29 （或者0b11101）, B = 15（或者0b01111）
輸出：2
```


### Example 2
```
輸入：A = 1，B = 2
輸出：2
```

* A，B範圍在[-2147483648, 2147483647]之間

```

## Solution  

### C++

* 時間複雜度 O(1) 1

* 空間複雜度 O(1) 

```
class Solution
{
public:
    int convertInteger(int A, int B)
    {
        int xorAB = A ^ B;
        int count = 0;
        for (int i = 0; i < 32; ++i)
        {
            if((1 << i) & xorAB)
                count++;
        }

        return count;
    }
};

int main()
{
    /* input*/

    /* Test*/
    Solution test;
    int ret = test.convertInteger(INT_MAX, INT_MIN);

    return 0;
}
```